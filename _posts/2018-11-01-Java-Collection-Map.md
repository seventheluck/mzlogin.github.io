---
layout: post
title: Java Map 01
categories: Java Map 01
description: Java Map 01
keywords: Java, Map
---

#### Map

##### Map Overview

```java
public interface Map<K,V> {
    // Query Operations

    // Returns the number of key-value mappings in this map. This value cannot more than Integer.MAX_VALUE.
    int size();

    // Returns if this map contains key-value mappings or not.
    boolean isEmpty();

    // Returns if this map contains a mapping for the specified key.
    boolean containsKey(Object key);

    // Returns if this map contains one or more values.
    boolean containsValue(Object value);

    // Returns the specified value with specified key int this map.
    V get(Object key);

    // Modification Operations

    // If the map previously contained a mapping for the key, the old value will be replaced by the new value. Returns the previous value.
    // If not, put the key-value mapping in the map. Returns null.
    V put(K key, V value);

    // If the map previously contained a mapping for the key, the old value will be removed. Returns the previous value.
    // If not, Returns null.
    V remove(Object key);


    // Bulk Operations

    // Copies all of the mappings from the target map.
    // If the target map is null or current map does not permit null keys or values, it will throw a NullPointerException.
    void putAll(Map<? extends K, ? extends V> m);

    // Removes all of the mappings from this map. This map will be empty.
    void clear();


    // Views

    // Returns a view of the keys contained in this map.
    // The set supports element removal, which removes the corresponding mapping from the map.
    // Removes the mapping from the map will removes corresponding key in the key set.
    Set<K> keySet();

    // Returns a view of the values contained in this map.
    // The collection supports element removal, which removes the corresponding mapping from the map.
    // Removes the mapping from the map will removes corresponding values in the collection.
    Collection<V> values();

    // Returns a view of the key-values contained in this map.
    // The set supports element removal, which removes the corresponding mapping from the map.
    // Removes the mapping from the map will removes corresponding key-values in the key set.
    Set<Map.Entry<K, V>> entrySet();

    interface Entry<K,V> {

        // Returns the key corresponding to this entry.
        K getKey();

        // Returns the value corresponding to this entry.
        V getValue();

        // Replaces the value corresponding to this entry.
        V setValue(V value);

        // Compares the entry's key and value, if entry1's key == entry2's key && entry1's value == entry2's value, returns true.
        boolean equals(Object o);

        // Returns the hash code for this map entry
        //(e.getKey()==null   ? 0 : e.getKey().hashCode()) ^ (e.getValue()==null ? 0 : e.getValue().hashCode())
        int hashCode();

        // Returns a comparator that compares {@link Map.Entry} in natural order on key.
        public static <K extends Comparable<? super K>, V> Comparator<Map.Entry<K,V>> comparingByKey() {
            return (Comparator<Map.Entry<K, V>> & Serializable)
                (c1, c2) -> c1.getKey().compareTo(c2.getKey());
        }

        // Returns a comparator that compares {@link Map.Entry} in natural order on value.
        public static <K, V extends Comparable<? super V>> Comparator<Map.Entry<K,V>> comparingByValue() {
            return (Comparator<Map.Entry<K, V>> & Serializable)
                (c1, c2) -> c1.getValue().compareTo(c2.getValue());
        }

        // Returns a comparator that compares {@link Map.Entry} by key using the given
        public static <K, V> Comparator<Map.Entry<K, V>> comparingByKey(Comparator<? super K> cmp) {
            Objects.requireNonNull(cmp);
            return (Comparator<Map.Entry<K, V>> & Serializable)
                (c1, c2) -> cmp.compare(c1.getKey(), c2.getKey());
        }

        // Returns a comparator that compares {@link Map.Entry} by value using the given
        public static <K, V> Comparator<Map.Entry<K, V>> comparingByValue(Comparator<? super V> cmp) {
            Objects.requireNonNull(cmp);
            return (Comparator<Map.Entry<K, V>> & Serializable)
                (c1, c2) -> cmp.compare(c1.getValue(), c2.getValue());
        }
    }

    // Comparison and hashing

    // 1. If the given object is also a map and the two maps represent the same mappings.
    // 2. If m1.entrySet().equals(m2.entrySet())
    // Two sets are equals is defined to be: if the specified object is also a set, the two sets
    // have the same size, and every member of the specified set is
    // contained in this set (or equivalently, every member of this set is
    // contained in the specified set).
    boolean equals(Object o);

    // Returns the hash code value for this map.  The hash code of a map is defined 
    // to be the sum of the hash codes of each entry in the map's entrySet.
    int hashCode();

    // Defaultable methods

    // Returns the value to which the specified key is mapped, 
    // or returns default value if this map contains no mapping for the key.
    default V getOrDefault(Object key, V defaultValue) {
        V v;
        return (((v = get(key)) != null) || containsKey(key))
            ? v
            : defaultValue;
    }

    // The default implementation is equivalent to, for this :
    // for (Map.Entry<K, V> entry : map.entrySet())
    //     action.accept(entry.getKey(), entry.getValue());
    // }
    default void forEach(BiConsumer<? super K, ? super V> action) {
        Objects.requireNonNull(action);
        for (Map.Entry<K, V> entry : entrySet()) {
            K k;
            V v;
            try {
                k = entry.getKey();
                v = entry.getValue();
            } catch(IllegalStateException ise) {
                // this usually means the entry is no longer in the map.
                throw new ConcurrentModificationException(ise);
            }
            action.accept(k, v);
        }
    }

    // The default implementation is equivalent to, for this :
    // for (Map.Entry<K, V> entry : map.entrySet())
    //     entry.setValue(function.apply(entry.getKey(), entry.getValue()));
    // }
    default void replaceAll(BiFunction<? super K, ? super V, ? extends V> function) {
        Objects.requireNonNull(function);
        for (Map.Entry<K, V> entry : entrySet()) {
            K k;
            V v;
            try {
                k = entry.getKey();
                v = entry.getValue();
            } catch(IllegalStateException ise) {
                // this usually means the entry is no longer in the map.
                throw new ConcurrentModificationException(ise);
            }

            // ise thrown from function is not a cme.
            v = function.apply(k, v);

            try {
                entry.setValue(v);
            } catch(IllegalStateException ise) {
                // this usually means the entry is no longer in the map.
                throw new ConcurrentModificationException(ise);
            }
        }
    }

    
    // If the vaule with specified key is null, put new value.
    // In here, absent means the value is null.
    default V putIfAbsent(K key, V value) {
        V v = get(key);
        if (v == null) {
            v = put(key, value);
        }

        return v;
    }

    // Remove key and vaule, if map contains key-value mapping.
    default boolean remove(Object key, Object value) {
        Object curValue = get(key);
        if (!Objects.equals(curValue, value) ||
            (curValue == null && !containsKey(key))) {
            return false;
        }
        remove(key);
        return true;
    }

    // Replace the value, if the map contains the key-value mapping.
    default boolean replace(K key, V oldValue, V newValue) {
        Object curValue = get(key);
        if (!Objects.equals(curValue, oldValue) ||
            (curValue == null && !containsKey(key))) {
            return false;
        }
        put(key, newValue);
        return true;
    }
    // If the map contains the specified key, replace by new value.
    default V replace(K key, V value) {
        V curValue;
        if (((curValue = get(key)) != null) || containsKey(key)) {
            curValue = put(key, value);
        }
        return curValue;
    }

    // If the value of specified key is null, compute the value by key.
    default V computeIfAbsent(K key,
            Function<? super K, ? extends V> mappingFunction) {
        Objects.requireNonNull(mappingFunction);
        V v;
        if ((v = get(key)) == null) {
            V newValue;
            if ((newValue = mappingFunction.apply(key)) != null) {
                put(key, newValue);
                return newValue;
            }
        }

        return v;
    }

    // If the value of specified key is present, replace the old value by the new value.
    default V computeIfPresent(K key,
            BiFunction<? super K, ? super V, ? extends V> remappingFunction) {
        Objects.requireNonNull(remappingFunction);
        V oldValue;
        if ((oldValue = get(key)) != null) {
            V newValue = remappingFunction.apply(key, oldValue);
            if (newValue != null) {
                put(key, newValue);
                return newValue;
            } else {
                remove(key);
                return null;
            }
        } else {
            return null;
        }
    }

    // Compute new value by key and old value, if the new value is not null, put the new value - key mapping.
    // If the new value is null and the old value is not null, remove key-value mapping of the map.
    default V compute(K key,
            BiFunction<? super K, ? super V, ? extends V> remappingFunction) {
        Objects.requireNonNull(remappingFunction);
        V oldValue = get(key);

        V newValue = remappingFunction.apply(key, oldValue);
        if (newValue == null) {
            // delete mapping
            if (oldValue != null || containsKey(key)) {
                // something to remove
                remove(key);
                return null;
            } else {
                // nothing to do. Leave things as they were.
                return null;
            }
        } else {
            // add or replace old mapping
            put(key, newValue);
            return newValue;
        }
    }

    // If current map contains a null value of specified key, put new value - key mapping.
    // If current map contains the not null value of specified key, compute the new value, if new value is not null, put new value - key mapping.
    // If the new value is null, remove the key-value mapping of the map.
    default V merge(K key, V value,
            BiFunction<? super V, ? super V, ? extends V> remappingFunction) {
        Objects.requireNonNull(remappingFunction);
        Objects.requireNonNull(value);
        V oldValue = get(key);
        V newValue = (oldValue == null) ? value :
                   remappingFunction.apply(oldValue, value);
        if(newValue == null) {
            remove(key);
        } else {
            put(key, newValue);
        }
        return newValue;
    }
}
```

#### HashMap

##### HashMap Overview
HashMap is an implementation of Map interface.

###### Initial capacity
The default initial capacity is 16(1 << 4) - MUST be a power of two.
```java
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4;
```
###### Maximum capacity
The maximum capacity, used if a higher value is implicitly specified by either of the constructors with arguments. MUST be a power of two <= 1<<30.
```java
    static final int MAXIMUM_CAPACITY = 1 << 30;
```
###### Load factor
The load factor used when none specified in constructor.
```java

    static final float DEFAULT_LOAD_FACTOR = 0.75f;
```
###### Treeify threshold
```java
    static final int TREEIFY_THRESHOLD = 8;
```
##### Constructor method
```java
    public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
    }

    public HashMap(int initialCapacity) {
        this(initialCapacity, DEFAULT_LOAD_FACTOR);
    }

    public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
    }    
```
![map](/images/my_posts/java_collection_map/map1.jpg)
Cite: 
JDK 8.
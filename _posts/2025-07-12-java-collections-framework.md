---
title: Java - 컬렉션 프레임워크
date: 2025-07-12 18:15:00 +0900
categories: [Programming Languages, Java]
tags: [java]
image: /assets/img/posts/CollectionsFramework.png
---

# Collections Framework

---

## 컬렉션 프레임워크(Collections Framework)란?

> 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합
> {: .prompt-tip }

### 컬렉션 프레임워크 핵심 인터페이스

컬렉션 프레임워크에서는 컬렉션데이터 그룹을 크게 3가지 타입이 존재한다고 인식하고 각 컬렉션을 다루는 데 필요한 기능을 가진 3개의 인터페이스를 정의하였다.

- List
- Set
- Map

그리고 List와 Set의 공통된 부분을 다시 뽑아서 새로운 인터페이스인 Collection을 추가로 정의하였다.

![](/assets/img/posts/CollectionsFramework.png)

| 인터페이스 | 특징                                                                                                                                 | 구현 클래스                                |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------ |
| List       | 순서가 있는 데이터의 집합.<br>데이터의 중복을 허용.                                                                                  | ArrayList, LinkedList, Stack, Vector 등    |
| Set        | 순서가 없는 데이터의 집합.<br>데이터의 중복을 허용하지 않음.                                                                         | HashSet, TreeSet 등                        |
| Map        | 키(key)와 값(value)의 쌍(pair)으로 이루어진 데이터의 집합.<br>순서는 유지되지 않으며, 키는 중복을 허용하지 않고, 값은 중복을 허용함. | HashMap, TreeMap, Hashtable, Properties 등 |

### Collection 인터페이스

| 메서드                                                          | 설명                                                                                                                                                                   |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| boolean add(Object o)<br>boolean addAll(Collection c)           | 지정된 객체(o) 또는 Collection(c)의 객체들을 Collection에 추가한다.                                                                                                    |
| void clear()                                                    | Collection의 모든 객체를 삭제한다.                                                                                                                                     |
| boolean contains(Object o)<br>boolean containsAll(Collection c) | 지정된 객체(o) 또는 Collection(c)의 객체들이 Collection에 포함되어 있는지 확인한다.                                                                                    |
| boolean equals(Object o)                                        | 동일한 Collection인지 비교한다.                                                                                                                                        |
| int hashCode()                                                  | Collection의 hash code를 반환한다.                                                                                                                                     |
| boolean isEmpty()                                               | Collection이 비어있는지 확인한다.                                                                                                                                      |
| Iterator iterator()                                             | Collection의 Iterator를 얻어서 반환한다.                                                                                                                               |
| boolean remove(Object o)                                        | 지정된 객체를 삭제한다.                                                                                                                                                |
| boolean removeAll(Collection c)                                 | 지정된 Collection에 포함된 객체들을 삭제한다.                                                                                                                          |
| boolean retainAll(Collection c)                                 | 지정된 Collection에 포함된 객체만 남기고 다른 객체들은 Collection에서 삭제한다.<br>이 작업으로 인해 Collection에 변화가 있으면 true를, 그렇지 않으면 false를 반환한다. |
| int size()                                                      | Collection에 저장된 객체의 개수를 반환한다.                                                                                                                            |
| Object[] toArray()                                              | Collection에 저장된 객체를 객체 배열(Object[])로 반환한다.                                                                                                             |
| Object[] toArray(Object[] a)                                    | 지정된 배열에 Collection의 객체를 저장해서 반환한다.                                                                                                                   |

### List 인터페이스

| 메서드                                                                         | 설명                                                                               |
| ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| void add(int index, Object element)<br>boolean addAll(int index, Collection c) | 지정된 위치(index)에 객체(element) 또는 컬렉션에 포함된 객체들을 추가한다.         |
| Object get(int index)                                                          | 지정된 위치(index)에 있는 객체를 반환한다.                                         |
| int indexOf(Object o)                                                          | 지정된 객체의 위치(index)를 반환한다. (List의 첫 번째 요소부터 순방향으로 찾는다.) |
| int lastIndexOf(Object o)                                                      | 지정된 객체의 위치(index)를 반환한다. (List의 마지막 요소부터 역방향으로 찾는다.)  |
| ListIterator listIterator()<br>ListIterator listIterator(int index)            | List의 객체에 접근할 수 있는 ListIterator를 반환한다.                              |
| Object remove(int index)                                                       | 지정된 위치(index)에 있는 객체를 삭제하고 삭제된 객체를 반환한다.                  |
| Object set(int index, Object element)                                          | 지정된 위치(index)에 객체(element)를 저장한다.                                     |
| void sort(Comparator c)                                                        | 지정된 비교자(comparator)로 List를 정렬한다.                                       |
| List subList(int fromIndex, int toIndex)                                       | 지정된 범위(fromIndex부터 toIndex)에 있는 객체를 반환한다.                         |

### Set 인터페이스

| 메서드                      | 설명                                        |
| --------------------------- | ------------------------------------------- |
| boolean add(Object element) | 주어진 객체를 저장                          |
| boolean contains(Object o)  | 주어진 객체가 저장되어 있는지 여부          |
| void clear()                | Collection의 모든 객체를 삭제한다.          |
| boolean remove(Object o)    | 지정된 객체를 삭제한다.                     |
| boolean isEmpty()           | Collection이 비어있는지 확인한다.           |
| Iterator iterator()         | Collection의 Iterator를 얻어서 반환한다.    |
| int size()                  | Collection에 저장된 객체의 개수를 반환한다. |


### Map 인터페이스

| 메서드                               | 설명                                                                              |
| ------------------------------------ | --------------------------------------------------------------------------------- |
| void clear()                         | Map의 모든 객체를 삭제한다.                                                       |
| boolean containsKey(Object key)      | 지정된 key객체와 일치하는 Map의 key객체가 있는지 확인한다.                        |
| boolean containsValue(Object value)  | 지정된 value객체와 일치하는 Map의 value객체가가 있는지 확인한다.                  |
| Set entrySet()                       | Map에 저장되어 있는 key-value쌍을 Map.Entry타입의 객체로 저장한 Set으로 반환한다. |
| boolean equals(Object o)             | 동일한 Map인지 비교한다.                                                          |
| Object get(Object key)               | 지정된 key객체에 대응하는 value객체를 찾아서 반환한다.                            |
| int hashCode()                       | 해시코드를 반환한다.                                                              |
| boolean isEmpty()                    | Map이 비어있는지 확인한다.                                                        |
| Set keySet()                         | Map에 저장된 모든 key객체를 반환한다.                                             |
| Object put(Object key, Object value) | Map에 value객체를 key객체에 연결(mapping)하여 저정한다.                           |
| void putAll(Map t)                   | 지정된 Map의 모든 key-value쌍을 추가한다.                                         |
| Object remove(Object key)            | 지정한 key객체와 일치하는 key-value객체를 삭제한다.                               |
| int size()                           | Map에 저장된 key-value쌍의 개수를 반환한다.                                       |
| Collection values()                  | Map에 저장된 모든 value객체를 반환한다.                                           |

### Map.Entry 인터페이스

| 메서드                        | 설명                                      |
| ----------------------------- | ----------------------------------------- |
| boolean equals(Object o)      | 동일한 Entry인지 비교한다.                |
| Object getKey()               | Entry의 key객체를 반환한다.               |
| Object getValue()             | Entry의 value객체를 반환한다.             |
| int hashCode()                | Entry의 해시코드를 반환한다.              |
| Object setValue(Object value) | Entry의 value객체를 지정된 객체로 바꾼다. |
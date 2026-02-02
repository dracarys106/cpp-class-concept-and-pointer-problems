# C Structures, Pointers & Memory

---

## 1. User Defined Data Type – `struct`

A **structure** is a user-defined data type used to group different data types under one name.

```c
struct node {
    int a;      // 4 bytes
    float b;    // 4 bytes
    char c;     // 1 byte
};
```

### Concepts Applied

* Groups heterogeneous data
* Memory allocated contiguously
* Accessed using `.` operator

---

## 2. Structure Size & Padding (Very Important)

From notes:

* `int` → 4 bytes
* `float` → 4 bytes
* `char` → 1 byte

Logical size = **9 bytes**

Actual size = **12 bytes** (due to **padding**)

### Key Concept: Structure Padding

* Compiler adds extra bytes for **alignment**
* Improves CPU access speed
* Size is always a multiple of largest data type

---

## 3. Nested Structures (Structure Inside Structure)

```c
struct node1 {
    float d;
    struct node e;
};
```

### Concepts Applied

* Structure as a member of another structure
* Size = size of all members combined
* `struct node` must be defined **before** use

---

## 4. Order of Definition (Compilation Rule)

❌ Invalid:

```c
struct node1 { struct node e; }; // node not defined yet
```

✅ Valid:

```c
struct node { ... };
struct node1 { struct node e; };
```

---

## 5. Structure Initialization (Single & Nested)

```c
struct node1 f = {10.25, {5, 20.45, 's'}};
```

### Rules

* Initialization must follow **member order**
* Nested structure requires nested braces
* Partial initialization is allowed

---

## 6. Accessing Members

```c
f.d       // float d
f.e.a     // nested member
```

Operators used:

* `.` → structure variable
* `->` → pointer to structure

---

## 7. `sizeof` Operator on Structures

```c
sizeof(struct node)    // valid
sizeof(struct node1)   // valid
sizeof(node)           // ❌ error
```

### Concept

* `struct` keyword is mandatory unless `typedef` is used

---

## 8. Invalid Initialization Inside Structure

```c
struct node {
    int a = 10;   // ❌ not allowed
};
```

### Rule

* Initialization is **not allowed inside structure definition**
* Allowed only at variable declaration

---

## 9. Structures with Character Pointers

```c
struct a {
    char *c1;
    char *c2;
};

struct b {
    char *c;
    struct a s1;
};
```

### Concepts

* Strings stored separately in memory
* Structure stores **addresses**, not string data
* Multiple pointers may refer to different memory blocks

---

## 10. Structure Initialization with Strings

```c
struct b s2 = {"Raipur", {"Kanpur", "Jaipur"}};
```

### Memory Concept

* String literals stored in read-only memory
* Structure stores pointer addresses

---

## 11. Structure Pointer (`->` Operator)

```c
struct b *p = &s2;
printf("%s", p->c);
```

### Concept

* `->` is shorthand for `(*p).member`

---

## 12. Array of Structures

```c
struct S1 {
    char *z;
    int i;
    struct S1 *p;
};

struct S1 a[3] = {
    {"Nagpur", 1, a+1},
    {"Raipur", 2, a+2},
    {"Kanpur", 3, a}
};
```

### Concepts Applied

* Array elements stored contiguously
* Self-referential structure
* Pointer linking between array elements

---

## 13. Self-Referential Structure

```c
struct S1 {
    char *z;
    int i;
    struct S1 *p;
};
```

### Why Needed?

* Used in linked lists, trees, graphs
* Enables dynamic data structures

---

## 14. Pointer Traversal Through Structures

```c
struct S1 *ptr = a;
for(int j = 0; j < 3; j++) {
    printf("%d", ptr->i);
    ptr = ptr->p;
}
```

### Concept

* Pointer movement follows logical links, not memory order

---

## 15. Difference Between Array & Pointer

```c
int a[3] = {10, 20, 30};
int *p = a;
```

| Array       | Pointer          |
| ----------- | ---------------- |
| Fixed size  | Can move         |
| Owns memory | Refers to memory |

---

## 16. Function with Structure Pointer

```c
typedef struct S1 {
    char *a;
    char *b;
} t;

void f1(t s);     // call by value
void f2(t *p);    // call by address
```
## 19. `sizeof` on Array vs Pointer

```c
char *str[] = {"Yoga","Do","Not","Die","Speak"};
```

* `sizeof(str)` → 5 × pointer size
* `sizeof(str[0])` → pointer size

---


# 📘 Cheat Sheet — Data Structures & Algorithms (DII 2026)

> อ.Suttinee · อ้างอิง *Introduction to Algorithms (CLRS) 3rd ed.* · อ่านก่อนสอบ

---

## 0. ภาพรวม & แนวคิดราก

- **Data Structure** = วิธีเก็บ/จัดระเบียบข้อมูลให้เข้าถึงและแก้ไขง่าย
- **Algorithm** = ลำดับขั้นตอนแปลง Input → Output ต้อง **terminate ได้ + ถูกต้องทุก input**
- **Linear** (เรียงเป็นเส้น): Array, List, Stack, Queue
- **Non-Linear** (เชื่อมหลายระดับ): Tree, Graph, Hash Table
- 🔑 **กฎทอง: "No single data structure is perfect"** — เลือกตามงานเสมอ
- 🔑 ฮาร์ดแวร์ = พลังดิบ / algorithm = ความฉลาด → ฮาร์ดแวร์แรง + algorithm ห่วย = ยังช้า

---

## 1. Stack & Queue

| | **Stack** | **Queue** |
|---|---|---|
| หลักการ | **LIFO** (เข้าทีหลังออกก่อน) | **FIFO** (เข้าก่อนออกก่อน) |
| operation | push / pop / peek / empty / size | enQueue(insert) / deQueue(remove) / peek |
| ตัวชี้ | `top` | `front` + `rear` |

**Stack (array):** เริ่ม `top = -1`
- push → `top++; list[top] = x;`
- pop → `x = list[top]; top--; return x;`

**Queue ปัญหา:** เลื่อนทุกตัวตอน deQueue เปลือง → ใช้ **Circular Array**
- index ถัดไป = `(rear + 1) % SIZE`

**ประยุกต์ Stack:** ตรวจวงเล็บสมดุล, ท่องกราฟ, เก็บ nested method calls, คำนวณ expression

⚠️ Edge case ที่ต้องคิด: pop ตอนว่าง? push ตอนเต็ม? ดู top ยังไง?

---

## 2. Linked List

แต่ละข้อมูลอยู่ใน **node** = `element` + pointer `next`; node สุดท้าย `next = null`

| | **Array** | **Linked List** |
|---|---|---|
| เข้าถึง | สุ่มด้วย index (เร็ว O(1)) | ไล่ทีละตัว (O(n)) |
| memory | ติดกัน, จองตอน compile (static) | กระจาย, จองตอน run (dynamic) |
| insert/delete | ช้า (ต้องเลื่อน) | **เร็ว — ขยับ pointer** |
| ขนาด | ตายตัว | ยืด/หดได้ |

**โค้ดหัวใจ:**
```java
// addFirst
Node temp = new Node(x);
temp.next = head;
head = temp;

// removeFirst  → node เก่ากลายเป็น garbage
head = head.next;

// ท่อง list
Node current = head;
while (current != null) {
    System.out.print(current.element + " ");
    current = current.next;
}

// getLast → วนจนกระทั่ง current.next == null
```

**ชนิดพัฒนาขึ้น:**
- **Tailed** = เพิ่ม `tail` → addLast เร็ว
- **Circular** = tail ชี้กลับ head → วนซ้ำได้
- **Doubly** = เพิ่ม `prev` → เดินถอยหลังได้ (ใช้ DNode)
- ⚠️ ยิ่งเพิ่ม pointer ยิ่งต้อง maintain มากขึ้น

> ทำไมเขียนเองทั้งที่มี API? → เพื่อเข้าใจการทำงาน + complexity จะได้ใช้ API ถูก

---

## 3. ADT & Generics

- **ADT** = ชนิดข้อมูลที่นิยามด้วย "ชุดค่า + ชุด operation" และ **ซ่อนวิธี implement** (black box)
- **Generics `<E>`** = class เก็บได้ทุกชนิด ไม่จำกัด int
  - `Vector<Integer>`, `Vector<String>`
  - ✅ ประโยชน์: compiler ตรวจ type mismatch **ก่อน** รัน
  - ⚠️ ใช้ primitive ตรงๆ ไม่ได้ ต้อง wrapper (`Integer` ไม่ใช่ `int`)
- **ADT พร้อมใช้ใน Java** (`java.util`): `List` (ArrayList), `Stack`, `Queue` (LinkedList / ArrayDeque / PriorityQueue)

---

## 4. Efficiency — Big O ⭐ (สำคัญสุด)

**ทำไมไม่จับเวลาจริง?** เครื่องต่างกัน / รันแต่ละครั้งต่างกัน / เร็วๆ วัดไม่แม่น → นับ **operation เทียบขนาด input (n)**

**Notation:** Θ (บน+ล่าง) · Ω (ล่าง) · **O (บน, ใช้บ่อยสุด)**

**กฎลัด:**
- คงที่ไม่สำคัญ: O(2n)→O(n), O(500)→O(1)
- พจน์เล็กไม่สำคัญ: O(n²+n+5)→O(n²)
- arithmetic / assignment / เข้าถึง array = O(1)
- **loop = ความยาว loop × งานข้างใน**

**ตัวอย่างวิเคราะห์:**
| โค้ด | จำนวน op | Big O |
|---|---|---|
| `return n*(n+1)/2;` | 3 (คงที่) | **O(1)** |
| loop รวม 1..n | 4n+2 | **O(n)** |
| `Math.min(n,5)` ใน loop | ≤5 | **O(1)** |
| nested loop `j<n` | n² | **O(n²)** |
| `i = i*2` | log₂n+1 | **O(log n)** |
| `i += 2` | n/2 | **O(n)** |
| nested `j<=i` → 1+2+…+n = n(n+1)/2 | | **O(n²)** |

**ลำดับเร็ว→ช้า:**
`O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)`

🔑 ผลลัพธ์เท่ากัน ≠ ประสิทธิภาพเท่ากัน (`loop` vs `สูตร`)

---

## 5. Recursion

**3 องค์ประกอบขาดไม่ได้:**
1. **Base Case** — เงื่อนไขหยุด (ไม่มี = stack overflow)
2. **Recursive Case** — เรียกตัวเองด้วย input เล็กลง
3. **Progress** — ขยับเข้าใกล้ base case ทุกครั้ง

**ตัวอย่าง + Big O:**
| method | สูตร | Big O |
|---|---|---|
| `factorial(n)` | `n * factorial(n-1)` | O(n) |
| `sum(start,end)` | `end + sum(start, end-1)` | O(n) |
| `fib(n)` | `fib(n-1)+fib(n-2)` | **O(2ⁿ)** ช้า! |
| `nFactorial` (loop+recursion) | | **O(n!)** |

🔑 อ่าน call stack: "บนลงล่าง เริ่ม main ก่อน" → ลงไปจนถึง base case แล้วคลายค่ากลับ (unrolling)

---

## 6. Tower of Hanoi (เคสศึกษา recursion)

**กติกา:** ย้ายทีละแผ่น · เฉพาะแผ่นบนสุด · ห้ามแผ่นใหญ่ทับแผ่นเล็ก

**Insight (ย้าย N แผ่น A→C):**
1. ย้าย N−1 แผ่น A→B (ใช้ C ช่วย)
2. ย้ายแผ่นใหญ่สุด A→C
3. ย้าย N−1 แผ่น B→C (ใช้ A ช่วย)

```java
void solve(int n, char from, char temp, char to) {
    if (n == 1) { print(from + " → " + to); return; }
    solve(n-1, from, to, temp);
    print(from + " → " + to);
    solve(n-1, temp, from, to);
}
```

- จำนวนการย้าย = **2ᴺ − 1** → **O(2ⁿ)**
- บทเรียน: โค้ดสวย ≠ เร็ว · iterative ไม่ได้เร็วขึ้น แค่ยาว/อ่านยาก · เลือกเครื่องมือให้ตรงกับปัญหา

---

## 7. Dynamic Programming (DP)

🔑 **"DP = Recursion + Memory" · "Solve once. Store. Reuse."**
ใช้เมื่อ: มี subproblem ซ้ำ + สร้างคำตอบจากคำตอบย่อยได้ + recursion ถูกแต่ช้า

**2 แนวทาง:**
- **Top-Down (Memoization)** — recursion + cache `memo[]`, เคยทำแล้วคืนทันที
- **Bottom-Up (Tabulation)** — เริ่มเล็กสุด ไล่สร้างด้วย loop `dp[0]…dp[n]`

**3 ปัญหาคลาสสิก:**
| ปัญหา | State | recurrence | Recursive | DP |
|---|---|---|---|---|
| Fibonacci | `dp[i]` | `dp[i]=dp[i-1]+dp[i-2]` | O(2ⁿ) | **O(n)** |
| Coin Change | `dp[a]`=เหรียญน้อยสุดยอด a | `dp[a]=min(dp[a], dp[a-coin]+1)` | exp | **O(amount×coins)** |
| 0/1 Knapsack | `dp[i][c]`=ค่ามากสุด i ชิ้นแรก จุ c | `max(skip=dp[i-1][c], take=val+dp[i-1][c-w])` | O(2ⁿ) | **O(items×cap)** |

**ขั้นตอนแก้ DP (7):** subproblem → state → base case → recurrence → top-down/bottom-up → เติม table → คืนคำตอบ

> Knapsack: แต่ละชิ้นเลือก take/skip · row 0 = 0 ทั้งหมด · ถ้าน้ำหนัก > ความจุ → copy แถวบน

---

## 8. 🎯 รายละเอียดที่ข้อสอบชอบออก (เพิ่มเติม)

### 8.1 นิยามทางการของ Asymptotic Notation (Lesson 6)
ทั้งสามนิยามด้วยการหา **ค่าคงที่ c และ n₀** ให้เงื่อนไขจริงสำหรับ n ≥ n₀:
- **O (Big O — ขอบบน):** `0 ≤ f(n) ≤ c·g(n)` → "เร็วสุดไม่เกินนี้"
- **Ω (Big Omega — ขอบล่าง):** `0 ≤ c·g(n) ≤ f(n)` → "ช้าสุดอย่างน้อยเท่านี้"
- **Θ (Big Theta — ขอบบน+ล่าง):** `0 ≤ c₁·g(n) ≤ f(n) ≤ c₂·g(n)` (ใช้ 2 ค่าคงที่)

**ตัวอย่างพิสูจน์ Big O:**
- `f(n) = 3` → O(1): ให้ c=3 → `0 ≤ 3 ≤ 3·1` ✓
- `f(n) = 4n+2` → O(n): ให้ c=6 → `0 ≤ 4n+2 ≤ 6n` (จริงตั้งแต่ n=1) ✓

### 8.2 Object References ใน Java (Lesson 3) — กับดักคลาสสิก ⚠️
`==` เปรียบเทียบ **reference (ที่อยู่)** ไม่ใช่ค่า
```java
Integer y = new Integer(20);
Integer w = new Integer(20);
if (w == y) ...   // FALSE — คนละ object คนละที่อยู่
w = y;            // ชี้ไป object เดียวกัน
if (w == y) ...   // TRUE
```
- primitive (`int x = 3`) เก็บ **ค่าจริง** / reference type (`Integer`, `String`, object) เก็บ **ที่อยู่**
- `new` = สร้าง object ใหม่เสมอ → ได้ที่อยู่ใหม่
- เทียบ "ค่า" ต้องใช้ `.equals()` ไม่ใช่ `==`

### 8.3 อัลกอริทึมตรวจวงเล็บสมดุลด้วย Stack (Lesson 2)
ไล่อ่านทีละตัว: เจอ `(` → **push** / เจอ `)` → **pop**
- ปลายทาง stack ว่าง = สมดุล ✓ · ถ้า pop ตอน stack ว่าง หรือจบแล้ว stack ไม่ว่าง = ไม่สมดุล ✗
- เช่น `((A*2))+(3+4)+(C+F))` ไม่สมดุล (วงเล็บปิดเกิน)

### 8.4 ทำไม recursion 2 กิ่ง = O(2ⁿ) (Binary Tree, Lesson 7)
recursion ที่เรียกตัวเอง 2 ครั้ง (เช่น fib) สร้าง tree ที่ **แต่ละชั้นมี node เป็น 2 เท่า**: ชั้น k มี 2ᵏ node → รวม ≈ 2ⁿ
- Fibonacci tree มี node ซ้ำ (red) เยอะ → ที่มาของการใช้ DP มาช่วย
- `nFactorial` (loop n รอบ × เรียกตัวเอง) → จำนวนครั้ง = n×(n-1)×… → **O(n!)**

### 8.5 ขอบเขตวิชาเต็ม — สไลด์ชุดนี้ = Part 1 เท่านั้น
**ยังไม่มีในไฟล์ (Part 2 โดย อ.Pop):** Searching & Sorting algorithms · Tree · Graph · Hash table
> เตรียมไว้ว่าข้อสอบ/บทเรียนถัดไปจะมีหัวข้อพวกนี้เพิ่ม

### 8.6 โจทย์/การบ้านที่แทรกในสไลด์ (มักออกสอบ)
- ปรับ Stack: จัดการ pop ตอนว่าง / push ตอนเต็ม / อ่านค่า top
- เขียน method ลบข้อมูลจาก array โดยไม่เหลือช่องว่างตรงกลาง
- เขียน method คัดลอก array หนึ่งไปอีก array
- วาดกราฟ complexity เทียบ n
- LinkedList: removeFirst, printAll (ทั้ง loop และ recursion), getSize, getLast
- เติมตาราง DP: coins=[1,2,5] amount=7 → คำตอบ dp = [0,1,1,2,2,1,2,2], ขั้นต่ำ 2 เหรียญ (5+2)

---

## ✅ 6 วิธีคิดหลักของวิชา
1. **Trade-off เสมอ** — ไม่มีอันที่ดีสุดทุกด้าน
2. **เขียนเองก่อนใช้ API** — เข้าใจลึก
3. **ถูกต้อง ≠ มีประสิทธิภาพ** — วัดด้วย Big O
4. **คิดเป็น input ขนาด n** — operation โตตาม n อย่างไร
5. **คิด edge case** — ว่าง/เต็ม/เกินขอบ
6. **ปัญหาใหญ่ = ปัญหาย่อยที่ซ้ำกัน** — รากของ Recursion + DP

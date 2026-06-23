# 🃏 Flashcards ถาม-ตอบ — DSA (DII 2026)

> วิธีใช้: ปิดส่วน **A:** แล้วลองตอบจากคำถามก่อน · ไฟล์ `flashcards-anki.csv` นำเข้า Anki ได้

---

## หมวด 0 — ภาพรวม

**Q1:** Data Structure คืออะไร?
**A:** วิธีเก็บและจัดระเบียบข้อมูลให้เข้าถึงและแก้ไขได้ง่าย

**Q2:** Algorithm ที่ถูกต้องต้องมีคุณสมบัติอะไร 2 อย่าง?
**A:** terminate ได้ (ไม่วนไม่จบ) + ให้ผลลัพธ์ถูกต้องสำหรับทุก input

**Q3:** ความต่างของ Linear กับ Non-Linear data structure?
**A:** Linear เรียงเป็นเส้น (Array, List, Stack, Queue); Non-Linear เชื่อมหลายระดับ (Tree, Graph, Hash Table)

**Q4:** "กฎทอง" ของ data structure คืออะไร?
**A:** No single data structure is perfect — ไม่มีอันที่ดีที่สุดทุกด้าน ต้องเลือกตามงาน

**Q5:** ฮาร์ดแวร์แรงแล้วทำไมยังต้องสน algorithm?
**A:** ฮาร์ดแวร์คือพลังดิบ algorithm คือความฉลาดที่ทำให้พลังนั้นมีประโยชน์ — ฮาร์ดแวร์แรงรัน algorithm ห่วยก็ยังช้า

---

## หมวด 1 — Stack & Queue

**Q6:** Stack ทำงานแบบใด? operation หลัก?
**A:** LIFO (เข้าทีหลังออกก่อน); push, pop, peek, empty, size

**Q7:** Queue ทำงานแบบใด? operation หลัก?
**A:** FIFO (เข้าก่อนออกก่อน); enQueue(insert), deQueue(remove), peek

**Q8:** Stack แบบ array เริ่มค่า top เท่าไร และ push ทำยังไง?
**A:** top = -1; push คือ `top++` แล้ว `list[top] = x`

**Q9:** ปัญหาของ Queue แบบ array ตอน deQueue คืออะไร แก้อย่างไร?
**A:** ถ้าเลื่อนทุกตัวจะเปลือง → ใช้ Circular Array, index ถัดไป = `(rear+1) % SIZE`

**Q10:** ยกตัวอย่างการประยุกต์ใช้ Stack
**A:** ตรวจวงเล็บสมดุล, ท่องกราฟ, เก็บ nested method calls, คำนวณ expression

---

## หมวด 2 — Linked List

**Q11:** Node ในlinked list ประกอบด้วยอะไร?
**A:** `element` (ข้อมูล) + pointer `next` (ชี้ node ถัดไป); ตัวสุดท้าย next = null

**Q12:** ข้อดีของ Linked List เหนือ Array?
**A:** insert/delete เร็ว (แค่ขยับ pointer), ขนาดยืด/หดได้, จองหน่วยความจำตอน run (dynamic)

**Q13:** ข้อดีของ Array เหนือ Linked List?
**A:** เข้าถึงแบบสุ่มด้วย index ได้ทันที O(1) (linked list ต้องไล่ทีละตัว)

**Q14:** โค้ด addFirst เขียนยังไง?
**A:** `Node temp = new Node(x); temp.next = head; head = temp;`

**Q15:** removeFirst ทำยังไง และ node เก่าเกิดอะไรขึ้น?
**A:** `head = head.next;` node เก่ากลายเป็น garbage ให้ JVM เก็บ

**Q16:** Tailed / Circular / Doubly linked list ต่างกันยังไง?
**A:** Tailed=เพิ่ม tail (addLast เร็ว); Circular=tail ชี้กลับ head (วนซ้ำ); Doubly=เพิ่ม prev (เดินถอยหลัง)

**Q17:** ทำไมต้องเขียน linked list เองทั้งที่มี API?
**A:** เพื่อเข้าใจการทำงานและ complexity จะได้ใช้ API ได้อย่างถูกต้องและมีประสิทธิภาพ

---

## หมวด 3 — ADT & Generics

**Q18:** ADT (Abstract Data Type) คืออะไร?
**A:** ชนิดข้อมูลที่นิยามด้วยชุดค่า + ชุด operation โดยซ่อนวิธี implement (มองเป็น black box)

**Q19:** Generics `<E>` มีประโยชน์หลักอะไร?
**A:** ทำให้ class เก็บได้ทุกชนิด + compiler ตรวจจับ type mismatch ได้ก่อนรัน

**Q20:** ข้อจำกัดของ Generics เรื่อง primitive?
**A:** ใช้ primitive ตรงๆ ไม่ได้ ต้องใช้ wrapper เช่น `Integer` ไม่ใช่ `int`

---

## หมวด 4 — Big O / Efficiency

**Q21:** ทำไมไม่วัดประสิทธิภาพด้วยเวลาจริง?
**A:** เครื่องต่างกัน, รันแต่ละครั้งต่างกัน, algorithm เร็วๆ วัดไม่แม่น → นับ operation เทียบขนาด input แทน

**Q22:** กฎลัด Big O 2 ข้อหลัก?
**A:** ค่าคงที่ไม่สำคัญ (O(2n)→O(n)) และพจน์เล็กไม่สำคัญ (O(n²+n)→O(n²))

**Q23:** loop ปกติ, nested loop, และ `i = i*2` ให้ Big O เท่าไร?
**A:** O(n), O(n²), O(log n) ตามลำดับ

**Q24:** เรียงลำดับความเร็วจากดีสุดไปแย่สุด
**A:** O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)

**Q25:** `n*(n+1)/2` กับ loop รวม 1..n ให้ผลเท่ากัน Big O ต่างกันยังไง?
**A:** สูตร = O(1), loop = O(n) → ผลถูกเท่ากันแต่ประสิทธิภาพต่างกัน

**Q26:** loop ที่ `i += 2` (เพิ่มทีละ 2) เป็น Big O อะไร?
**A:** O(n) — เพราะ n/2 ครั้ง แต่ตัดค่าคงที่ทิ้ง

---

## หมวด 5 — Recursion

**Q27:** 3 องค์ประกอบของ recursion?
**A:** Base case (เงื่อนไขหยุด), Recursive case (เรียกตัวเองด้วย input เล็กลง), Progress (ขยับเข้าใกล้ base case)

**Q28:** ไม่มี base case จะเกิดอะไรขึ้น?
**A:** recursion วนไม่จบ → stack overflow

**Q29:** Fibonacci แบบ recursion ธรรมดามี Big O เท่าไร และทำไม?
**A:** O(2ⁿ) เพราะคำนวณค่าเดิมซ้ำหลายครั้ง

**Q30:** factorial(n) มี Big O เท่าไร?
**A:** O(n)

---

## หมวด 6 — Tower of Hanoi

**Q31:** กติกา 3 ข้อของ Tower of Hanoi?
**A:** ย้ายทีละแผ่น, ย้ายเฉพาะแผ่นบนสุด, ห้ามวางแผ่นใหญ่ทับแผ่นเล็ก

**Q32:** insight การย้าย N แผ่นจาก A→C (3 ขั้น)?
**A:** 1) ย้าย N−1 แผ่น A→B 2) ย้ายแผ่นใหญ่สุด A→C 3) ย้าย N−1 แผ่น B→C

**Q33:** N แผ่นใช้กี่ครั้ง และ Big O เท่าไร?
**A:** 2ᴺ − 1 ครั้ง → O(2ⁿ)

**Q34:** เขียน Tower of Hanoi แบบ iterative ดีกว่า recursion ไหม?
**A:** ไม่เร็วขึ้น — แค่โค้ดยาวและอ่านยากกว่า; เลือกเครื่องมือให้ตรงกับปัญหา

---

## หมวด 7 — Dynamic Programming

**Q35:** ประโยคสรุป DP สั้นๆ?
**A:** "DP = Recursion + Memory" / "Solve once. Store. Reuse."

**Q36:** ควรใช้ DP เมื่อไร?
**A:** เมื่อมี subproblem ซ้ำ + สร้างคำตอบจากคำตอบย่อยได้ + recursion ถูกแต่ช้า

**Q37:** Top-Down (Memoization) ต่างจาก Bottom-Up (Tabulation) ยังไง?
**A:** Top-Down=recursion + cache; Bottom-Up=เริ่มเล็กสุดไล่สร้างขึ้นด้วย loop

**Q38:** Fibonacci recursion vs DP ลด Big O จากเท่าไรเป็นเท่าไร?
**A:** จาก O(2ⁿ) เหลือ O(n)

**Q39:** Coin Change recurrence เขียนยังไง?
**A:** `dp[a] = min(dp[a], dp[a-coin] + 1)`, base case dp[0]=0; Big O = O(amount × coins)

**Q40:** 0/1 Knapsack: dp[i][c] หมายถึงอะไร และ recurrence?
**A:** ค่ามากสุดจาก i ชิ้นแรก ความจุ c; `dp[i][c]=max(skip=dp[i-1][c], take=value+dp[i-1][c-weight])`; Big O=O(items×capacity)

**Q41:** 7 ขั้นตอนแก้ปัญหา DP?
**A:** subproblem → state → base case → recurrence → เลือก top-down/bottom-up → เติม table → คืนคำตอบ

---

## หมวด 7.5 — รายละเอียดที่ข้อสอบชอบออก

**Q42b:** นิยามทางการของ Big O เขียนยังไง?
**A:** มี c, n₀ ที่ทำให้ `0 ≤ f(n) ≤ c·g(n)` สำหรับทุก n ≥ n₀ (ขอบบน)

**Q42c:** Θ ต่างจาก O และ Ω อย่างไร?
**A:** O=ขอบบน (≤c·g), Ω=ขอบล่าง (≥c·g), Θ=ทั้งบนและล่าง ใช้ 2 ค่าคงที่ `c₁·g ≤ f ≤ c₂·g`

**Q42d:** พิสูจน์ว่า f(n)=4n+2 เป็น O(n) ยังไง?
**A:** ให้ c=6 → `0 ≤ 4n+2 ≤ 6n` จริงตั้งแต่ n=1 → เป็น O(n)

**Q42e:** ใน Java `new Integer(20) == new Integer(20)` ได้ผลอะไร ทำไม?
**A:** false — เพราะ `==` เทียบ reference (ที่อยู่) ไม่ใช่ค่า, new สร้าง object คนละตัว; เทียบค่าต้องใช้ .equals()

**Q42f:** primitive type กับ reference type เก็บอะไรต่างกัน?
**A:** primitive (int) เก็บค่าจริง; reference (Integer/String/object) เก็บที่อยู่ของ object

**Q42g:** ตรวจวงเล็บสมดุลด้วย stack ทำยังไง?
**A:** เจอ ( → push, เจอ ) → pop; จบแล้ว stack ว่าง=สมดุล, ถ้า pop ตอนว่างหรือจบแล้วไม่ว่าง=ไม่สมดุล

**Q42h:** ทำไม recursion ที่เรียกตัวเอง 2 ครั้งเป็น O(2ⁿ)?
**A:** สร้าง binary tree ที่แต่ละชั้นมี node เป็น 2 เท่า (ชั้น k มี 2ᵏ node) รวม ≈ 2ⁿ

**Q42i:** วิชานี้ Part 2 มีหัวข้ออะไรที่ยังไม่อยู่ในสไลด์ชุดนี้?
**A:** Searching & Sorting, Tree, Graph, Hash table (โดย อ.Pop)

---

## หมวด 8 — วิธีคิดหลัก

**Q42:** 6 วิธีคิดหลักของวิชานี้?
**A:** 1) Trade-off เสมอ 2) เขียนเองก่อนใช้ API 3) ถูกต้อง≠มีประสิทธิภาพ 4) คิดเป็น input ขนาด n 5) คิด edge case 6) ปัญหาใหญ่=ปัญหาย่อยซ้ำกัน

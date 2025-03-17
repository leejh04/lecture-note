# Chapter 2: Instruction Set Architecture
[목차](index.md)<br><br>

### 컴퓨터가 하는 일을 어떻게 나타낼까?
#### Architecture (ISA) level
- 자동차: 운전 매뉴얼과 사용법
    - 운전하기 위해서는 자동차 메카닉이 될 필요는 없다.
- 컴퓨터: 명렁어 집합 매뉴얼 (예시: Intel x86-64, Arm v8, RISC-V)
    - 컴퓨터를 사용하기 위해서 회로 디자이너가 될 필요는 없다.

#### Microarchitecture (implementation) level
- 자동차의 디자인에는 전기 및 기계적 구성 요소가 있다.
- 컴퓨터의 설계에는 datapath 및 control logic unit 구성 요소가 있다.

#### circuit level
- 자동차: metal sheets, cranks, shafts, gears, ...
- 컴퓨터, 게이트, 와이어, 반도체, 트랜지스터, ...

### Stored Program (von Neumann) Architecture
- stored-program architecture
    - 명령어는 선형 메모리에 들어 있다.
        - 명렁어와 데이터는 메모리에 있다.
    - 명렁어는 데이터처럼 수정될 수 있다.
        - 둘다 0과 1로 구성되어 있다.

- Sequential instruction processing
    - Program Counter는 현재 명령어의 위치를 가리킨다.
    - 명령어는 메모리에서 가져와서 실행된다.
    - program counter is advanced (according to instruction)
    - 반복한다.

### von Neumann vs. Dataflow
폰 노이만 구조
- 프로그램의 순서?
- 저장소 위치?

Dataflow: 명령어가 dataflow depenced에 의해 정렬되어 있다.
- 각 명령어는 누가 결과를 받아야 되는지 명시되어 있다.
- 명령어는 모든 피연산자들을 받았을때면 언제든지 실행될 수 있다.

## Instruction Set Architecture (ISA) "User's manual for the computer"
### ISA에는 무엇이 명시되어 있고, 결정되어 있는가?
- Data Types
    - Encoding and representation
- Memory Model
- Program Visible State
    - General registers
    - Memory space
    - program counter
    - processor status
- Instruction Set
    - instructions and formats
    - addressing modes
    - data structures
- System Model
    - States
    - Privilege
    - Interrupts
    - IO
- External Interfaces
    - IO
    - Management

### Programmer Visible State
#### Memory
- array of storage locations indexed by an address

#### Registers
- Given special names in the ISA (as opposed to address)
- general vs. special purpose

#### Program Counter
- Memory address of the current instruction
다시 말해, 명렁어, 즉 프로그램은 programmer visible state의 값들을 어떻게 바꿔야 하는지 명시한다.

### General Instruction Classes
#### 산술 논리 연산 (예시: add, sub, and, or)
- 대체로 정수형 또는 실수형 명렁어로 분류될 수 있다.
1) 특정 위치에서 피연산자들을 가져온다.
2) 연산자들을 함수로 연산한다.
3) 특정 위치에 결과를 저장한다.
4) 다음 명렁어 위치로 pc를 업데이트한다.

#### Data movement operations (예시: move, load, store)
1) 특정 위치에서 피연산자들을 가져온다.
2) 특정 위치에 피연산자의 값들을 저장한다.
3) pc를 다음으로 옮긴다.

#### Control flow operations (예시: branch, jump)
1) 특정 위치에서 피연산자들을 가져온다.
2) branch 조건과 target address를 계산한다.
3) branch 조건이 참이면, pc를 target address로, 거짓이면, 다음 명령어로 업데이트한다.

### Atomicity of an Instruction
- 모든 명령어들은 소프트웨어 관점에서 완전히 실행되었거나, 아직 실행되었거나 둘중 하나이다.
- 다시 말해, 명령어에 의한, programmer visible state의 부분적인 업데이트는 관측되어서는 절대 안된다.
- 예시: semantics of a RISC-V instruction "ADDI x4, x5, 10"
    - GPR[x4] <- GPR[x5] + 10
    - PC <- PC + 4

### 초기의 ISA: EDSAC (1949)
- Single accumulator architecture

### Evolution of "Register" Architecture
- accumulator
- accumulator + address registers
- General-purpose registers

### Operand Sources?
- 피연산자의 개수
    - mondaic (예시: EDSAC)
    - dyadic (예시: IBM 360)
    - triadic (예시: MIPS)
- can ALU operands be in memory?
    - Yes (예시: x86/VAX/CISC)
    - No (예시: MIPS/RISC) -> load-store architecture
- How many different variations
    - a very few (예시: MIPS/RISC)
    - a lot (예시: x86)
    - everything goes (예시: VAX)

### Memory Addressing Modes
- absolute
    - immediate value를 주소로 사용.
- register indirect
    - GPR의 값을 주소로 사용.
- displaced of based
    - GPR+offset의 값을 주소로 사용.
- indexed
    - GPR[r_base]+GPR[r_index]의 값을 주소로 사용.
- memory indirect
    - M[GPR]의 값을 주소로 사용.
- auto inc/decrement
    - GPR[r_base]의 값을 주소로 사용하고, GPR[r_base]를 더하거나 뺀다.

### VAX-11: ISA in Mid-life Crisis
- 최초의 상업적인 32비트 머신.

### RISC (Reduced Instruction Set Computer)
- Simple operations
    - 2개의 입력, 1개의 출력. 산술 논리 연산.
    - few alternatives exist to do the same thing
- Simple data movements
    - ALU의 피연산자들은 레지스터이다.
    - 레지스터들의 값들을 연산하고, 그 값을 레지스터에 저장한다. (need a larage register file)
    - 메모리는 오직 load와 store 명령어로만 접근 가능하다. -> Load-store architecture
- Simple branches
    - branch 조건문과 target address가 제한적?
- Simple instruction encoding
    - 모든 명령어는 같은 비트 크기로 인코딩된다.
    - 포맷이 몇개 없다.

### Evoluation of ISA

## What if you have to design an ISA>
### Open-Ended Design: Extrapolation and Anticipation
- 비동기적인 연산의 구성요소
    - abstract out exact time, performance, etc. to allow (1) changing technology and (2) relative speed of componenets
- parameterization of storage capacity, multi-CPU, multi-I/O, etc.
- permit future extensions by "reserving" spare bits in instruction encoding
- standard interfaces for expansion sub-systems

### General Purpose
- General Purpose = effective support for "large and small, separate and mixed applications" in many domains

- 어떻게?
    - code-independent operation
        - no special interpretation of bit pattern in data
        - except where essential
    - support full generality of logic manipulation on bit and data entities
    - fine-grain memory addressability (예시: byte-addressability)

### Inter-Model Compatibility
- strict program compatibility
- invalid progrms are not constinrn to iyear lsuam reulst

### Wrap-up: Terminologies
- Instruction Set Architecture (ISA)
    - 프로그래머에 의해 관측 가능하고, 통제할 수 있는 기계의 행동.
- Instruction Seet
    - 컴퓨터가 이해 가능한 명령어의 집합.
- Machine code
    - 바이너리 형식으로 인코딩 된 명령어의 모음.
    - 하드웨어가 직접 사용할 수 있다?
- Assembly code
    - 명령어를 text 형식으로 나타낸것들.
    - 어셈블러에 의해 machine code로 변환된다.
    - 대략 기계어와 1대1 대응이 된다.

### RISC-V Programmer Visible State (RV32I)
- 다른 말로, "Architectual state"라고도 한다.
    - Program counter (32비트)
    - GPR (각각 32비트, 32개) (x0~x31, x0는 항상 0)
    - Memory (1바이트씩 2^32개. 즉 32bit address. 4gitabytes)
- 더 많은 레지스터를 사용하지 않는 이유는?
    - 디자인 원리 1: smaller is faster

### Data Format
- doubleword(64비트), word(32비트), halfword(16비트), byte(8비트)
- floating-point numbers: single(32비트), double(64비트)

### Exercise: Instruction Representation
- 어떻게 명령어를 0과 1로 나타내는가?
- 피연산자에 immediate value를 사용한다면?
- load? store?
- 디자인 원리 2: simplicity favors regularity
    - 규칙성은 구현을 더욱 간단하게 만들어준다.
    - 단순함은 더 낮은 비용으로 높은 성능을 가지도록 해준다.

### RISC-V Insturction Formats
- R-type: 산술 명령
    - funct7(7) rs2(5) rs1(5) funct3(3) rd(5) opcode(7)
- I-type: load, immediate 산술 명령
    - imm(12) rs1(5) funct3(3) rd(5) opcode(7)
- S-type: store
    - imm(7) rs2(5) rs1(5) funct3(3) imm(5) opcode(7)
- SB-type: 조건부 분기
    - imm(7) rs2(5) rs1(5) funct3(3) imm(5) opcode(7)
- UJ-type: 점프
    - imm(20) rd(5) opcode(7)
- U-type: upper immediate
    - imm(20) rd(5) opcode(7)
- store와 load의 형식이 다른 이유는?
    - 구현을 더 단순하게 하기 위함이다.
    - load와 store 모두 레지스터 2개를 입력받지만 다르다.
    - load는 메모리에서 값을 가져와서 레지스터에 쓰는 것이고,
    - store는 레지스터의 값을 메모리에 저장하는 것이다.
    - 이때, rd는 write할 레지스터를 나타내며,
    - rs는 read할 레지스터를 나타낸다.
    - 구현의 규칙성을 위해 형식을 구분한 것이다.
- simple decoding
    - 각 명령은 형식에 관계없이 4바이트이며, 항상 4바이트 정령이다. (LSB == 2'b00)
    - 포맷과 필드는 readily extractable하다.

### Register-Register ALU Instruction (R-type)
- Assembly example: ADD rd, rs1, rs2
- encoding: funct7(7) rs2(5) rs1(5) funct3(3) rd(5) opcode(7)
- semantics
    - GRP[rd] <- GRP[rs1] (OP) GRP[rs2]
    - PC <- PC + 4
- Variations
    - 산술: ADD, SUB
    - 비교: SLT, SLTU (Set if Less Than)
    - 논리: AND, OR, XOR
    - Shift: SLL, SRL SRA
- Exception: none (ignore carry and overflow)

### Assembly Programming Example (1)
- High-level code:
f = (g + h) - (i + j);
x19 x20 x21   x22 x23
_      x5       x6

- Assembly code:
    - GPR[x5] <- GPR[x20] + GPR[x21]
    - GPR[x6] <- GPR[x22] + GPR[x23]
    - GPR[x19] <- GPR[x5] - GPR[x6]
    - PC <- PC + 4

### Register-Immediate ALU Instruction (I-type)
- Assembly example: ADDI rd, rs1, imm_12
- Encoding: imm(12) rs1(5) funct3(3) rd(5) opcode(7)
- semantics
    - GRP[rd] <- GRP[rs1] (OP) sign-extend(imm)
    - PC <- PC + 4
- Variations
    - 산술: ADDI (no SUBI, 단순히 음수를 더하면 되기 때문)
    - 논리: ANDI, ORI, XORI
    - 비교: SLTI, SLTIU
- Exception: none (igonore carry and overflow)

### Shift Instructions (I-type)
- slightly different format
    - imm(7) shamt(5) rs1(5) funct3(3) rd(5) opcode(7)
    - imm[11:5], imm[4:0]
- Semantics:
    - GPR[rd] <- (GPR[rs1] shifted by shamt)
    - PC <- PC + 4
- shamt로 5비트만 쓰는 이유?
- 디자인 원리 3: good design demands good compromises
    - 다른 포맷은 디코딩을 복잡하게 만들지만, 명령어르 32비트로 맞추게 해준다.
    - common case를 더 빠르게 처리하도록 (immediate value가 작을 때, memory access가 없다.)
    - 포맷을 최대한 비슷하게 만들어라.

### What about Large Constants?
- 대부분의 상수들은 작다.
    - 12비트면 대체로 충분하다.
- 32비트 상수가 쓰고 싶다면, LUI를 사용. (Load Upper Immediate)
    - lui rd, constant
    - rd의 상위 20비트에 20비트 상수를 복사한다.
    - rd의 하위 12비트를 0로 초기화.

### RISC-V: Load-Store Architecture
- classes of main instructions
    - load/store insturction
        - 레지스터와 메모리 사이의 데이터 이동
    - ALU instruction 
        - 피연산자들은 항상 레지스터에 들어 있다.
    - control flow instruction
        - PC를 조작. (branch, jump)
        - 메모리나 레지스터에는 변화가 없다.
- simple instruction set (RISC vs. CISC)
- performance and energy-efficiency favors simplicity
- cf. other architectures
    - accumulator-based architecture
    - provice register-memory ALU instruciton in CISC (예시: x86)

### Load Instructions (I-type)
- Assembly example: LW rd, offset(base)
- encoding:
    - imm(12) rs1(5) funct3(3) rd(5) opcode(7)
- semantics:
    - byte_address_32 = sign-extend(offset) + GPR[base]
    - GPR[rd] <- MEM[byte_address_32]
    - PC <- PC + 4
- Exceptions: will be discussed later
- variations:
    - LW (word), LH (halfword), LB (byte): sign-extend
    - LHU, LBU: zero-extend

### Big Endian vs. Litte Endian
- Big-endian: 순서대로? (예시: IBM z/Architecture, 모토로라)
- Little-endain: 역순으로? (예시: RISC-V, x86)

### Data Alignment in Memory
- RISC-V에서는
    - 데이터 접근을 위해서는, unaligned 접근도 허용되나, 느리다.
    - 명령어 접근을 위해서는 unaligned 접근이 허용되지 않는다.
- 다른 아키텍처 (예시:MIPS)는 data에서도 unaligned 접근이 허용되지 않는다. 그러나, 여러 명령어의 조합으로 수행 가능하다.

### Store Instructions (S-type)
- Assembly example (Store Word): SW rs2, offset(base)
- encoding:
    - imm[11:5](7) rs2(5) rs1(5) funct3(3) imm[4:0](5) opcode(7)
- semantics:
    - byte_address_32 = sign-extend(imm) + GPR[rs1]
    - MEM[byte_address_32] <- GPR[rs2]
    - PC <- PC + 4
- exceptions: will be discussed later
- Variations:
    - SW(Word), SH(Halfword), SB(byte)

### Assembly Programming Example (2)
- High-level code:
A[30] = h + A[30] + 1;
        x21  x10
              x9
           x9
               x9

lw x9, x10, 30
add x9, x9, x21
add x9, x9, 1
sw x9, 30(x10)

### Control Flow Instructions
- if, else

### Conditional Branch Instructions (SB-type)
- Assmebly example (Branch if EQual): BEQ rs1, rs2, imm13
- Encoding:
    - imm[12,10:5](7) rs2(5) rs1(5) funct3(3) imm[4:1,11](5) opcode(7)
    - 이때, 명령어는 항상 aligned 되어 있으므로, 하위 2비트는 0이다.
    - 즉, imm[0] == 0 이다.
- Semantics:
    - Target = PC + sign-extend(imm13)
    - if GPR[rs1] == GPR[rs2] then PC <- target, else PC <- PC + 4
- Exception: misaligned target (4-byte) if taken
- Variations:
    - BEQ, BNE, BLT, BGE (signed variations)
    - BLTU, BGEU

### Assembly Programming Example (3)
- High-level code:
    if (i==j) f = g + h:
    else f = g - h;

BEQ x22, x23, else

add x19, x20, x21
else:
sub x19, x20, x21

### Jump Instruction (UJ-type)
- jump and link assembly: JAL rd, imm21
- encoding
    - imm[20, 10:1, 11, 19:12] rd(5) opcode(7)
- semantics:
    - target = PC + sign-extend(imm21)
    - GPR[rd] <- PC + 4
    - PC <- target
- Exception: misaligned target(4-byte)

### Jump Indirect Instruction (I-type)
- Jump and Link Register assembly: JALR rd, imm12(rs1)
- Encoding:
    - imm12(12) rs1(5) funct3(3) rd(5) opcode(7)
- semantics:
    - target = GPR[rs1] + sign-extend(imm12)
    - target &= 0xfffffffE
    - GPR[rd] <- PC + 4
    - PC <- target
- Usages:
    - procedure return jalr x0, 0(x1) // return to GPR[x1]
    - computed jumps (예시: case/switch statements)

### RISC-V Instruction Formats Overview

### Immediate Generation

### Cf. x86 Instruction Encoding Examples

### Caller and Callee Saved Registers

### RISC-V Register Usage Convention

### Calling Conventtion

### Memory Usage Convention

### RISC-V Addressing Summary


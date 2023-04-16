[MIPS Register]

$0 = Always 0

$at = The Assembler Temporary used by the assembler in expanding pseudo-ops.

$v0, $v1 = 리턴값 저장. 1 word 인 경우 $v0 만 사용. 초과할 경우 $v1 과 나눠서 저장

$a0-$a3 = 함수 인자값 저장. 초과할 경우 스택에 저장

$t0-$t9 = 임시 저장 레지스터

$s0 - $s7 = 저장 용 레지스터 – 함수 호출 중 불변

$k0, $k1 = 커널에서 사용하는 레지스터

$gp = 전역 포인터 레지스터

$sp = 스택 포인터

$fp = 함수 프레임 포인터 ($s8)

$ra = 서브루틴 호출 시 반환 주소 저장

 

[MIPS 주요 명령어]

addiu [addiu A B C] = [A <- B + C]

sw [sw A B] = [A ->B]

lw [lw A B] = [A <- B]

li(load immediate) [li A B] = [A <- B]

move [move A B] = [A <- B]

movn [movn A B C] = [if C != 0 then A <- B]

la [la A B] = [A <- B’s Addr]

lb [lb $a, (0)$s0] = $a 에 byte 단위로 데이터 로드

sb [sb $a, (100)$s0] = *($s0 + 100) 에 $a 저장

jal [jal A] - 다음 명령어의 주소를 $ra에 저장하고, A로 점프

bal [bal function] = function call = jalr

beq [beq A B L] = A와 B가 같으면 L로 점프

beqz [beqz R L] = R이 0이면 L로 점프

bne [bne A B L] = A와 B가 다르면 L로 점프

bnez [bnez R, L] = 레지스터 R이 0이 아니면 L로 점프

lui [lui A, 0x47] = A 레지스터 상위 2byte에 0x47 저장

0x90+var_74($fp) 와 같이 괄호가있을 경우 $fp+(0x90+var_74) 와 같은 표현이다.

slt [slt rd, rs, rt] = rd <= (rs < rt) ? 1 : 0

sll [sll $a, 1] = $a << 1



[MIPS 함수 호출 과정]

$ra 에 caller 의 return address 저장 (마지막 호출 함수의 경우 저장 안할 수 있음)

$a0 ~ $a3 에 인자값 저장 인자가 4개를 초과할 경우 초과한 만큼 스택에 저장

func(param1, param2, param3, param4) 일 경우 $a0 = param1, $a1 = param2, $a2 = param3, $a3 = param4 가 들어간다.

bal, jal, jalr 등 으로 함수 호출

return 값은 $v0 (4byte 초과시 $v1 에 나눠서 저장)

호출시 $ra 값 스택에 백업

$s0 ~ $s7도 필요한 경우 스택에 백업

![image](https://user-images.githubusercontent.com/58906858/232273243-3a186afb-1432-4eff-8091-c29c8e613be1.png)

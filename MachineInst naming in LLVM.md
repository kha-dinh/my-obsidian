- A single instruction from the architecture manual is often modeled as multiple
target instructions, depending upon its operands.  For example, a manual might
describe an add instruction that takes a register or an immediate operand.  An
LLVM target could model this with two instructions named ``ADDri`` and
``ADDrr``.
# Learn Chipyard System

## Step 1: Learn the basics chisel, follow [chisel-bootcap](https://mybinder.org/v2/gh/freechipsproject/chisel-bootcamp/master).


### 1.1 Getting Started

Try it out [HERE](https://mybinder.org/v2/gh/freechipsproject/chisel-bootcamp/master)! No local installation required!

If you want to try it out locally, [look at installation instructions here](Install.md).


### 1.2 Some helper functions.

    source/load-ivy.sc

```scala
// Convenience function to invoke Chisel and grab emitted Verilog.
def getVerilog(dut: => chisel3.core.UserModule): String = {
  import firrtl._
  return chisel3.Driver.execute(Array[String](), {() => dut}) match {
    case s:chisel3.ChiselExecutionSuccess => s.firrtlResultOption match {
      case Some(f:FirrtlExecutionSuccess) => f.emitted
    }
  }
}

// Convenience function to invoke Chisel and grab emitted FIRRTL.
def getFirrtl(dut: => chisel3.core.UserModule): String = {
  return chisel3.Driver.emit({() => dut})
}


def visualize(gen: () => chisel3.RawModule): Unit = {
    val (moduleView, instanceView) = generateVisualizations(gen)
    html(moduleView)
}

def visualizeHierarchy(gen: () => chisel3.RawModule): Unit = {
    val (moduleView, instanceView) = generateVisualizations(gen)
    html(instanceView)
}

```

## Step 2: Learn basic chisel module[(chisel-tutorial)](https://github.com/ucb-bar/chisel-tutorial)

```scala
// See LICENSE.txt for license details.
package examples

import chisel3.iotesters.{Driver, TesterOptionsManager}
import utils.TutorialRunner

object Launcher {
  val examples = Map(
      "Combinational" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Combinational(), manager) {
          (c) => new CombinationalTests(c)
        }
      },
      "Functionality" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Functionality(), manager) {
          (c) => new FunctionalityTests(c)
        }
      },
      "Parity" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Parity(), manager) {
          (c) => new ParityTests(c)
        }
      },
      "Tbl" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Tbl(), manager) {
          (c) => new TblTests(c)
        }
      },
      "Life" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Life(12, 12), manager) {
          (c) => new LifeTests(c)
        }
      },
      "Risc" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Risc(), manager) {
          (c) => new RiscTests(c)
        }
      },
      "Darken" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Darken(), manager) {
          (c) => new DarkenTests(c, getClass.getResourceAsStream("/in.im24"), "o" + "u,t.im24")
        }
      },
      "Adder" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Adder(8), manager) {
          (c) => new AdderTests(c)
        }
      },
      "Adder4" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Adder4(), manager) {
          (c) => new Adder4Tests(c)
        }
      },
      "SimpleALU" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new SimpleALU(), manager) {
          (c) => new SimpleALUTests(c)
        }
      },
      "FullAdder" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new FullAdder(), manager) {
          (c) => new FullAdderTests(c)
        }
      },
      "ByteSelector" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new ByteSelector(), manager) {
          (c) => new ByteSelectorTests(c)
        }
      },
      "GCD" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new GCD, manager) {
          (c) => new GCDTests(c)
        }
      },
      "HiLoMultiplier" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new HiLoMultiplier(), manager) {
          (c) => new HiLoMultiplierTests(c)
        }
      },
      "ShiftRegister" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new ShiftRegister(), manager) {
          (c) => new ShiftRegisterTests(c)
        }
      },
      "ResetShiftRegister" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new ResetShiftRegister(), manager) {
          (c) => new ResetShiftRegisterTests(c)
        }
      },
      "EnableShiftRegister" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new EnableShiftRegister(), manager) {
          (c) => new EnableShiftRegisterTests(c)
        }
      },
      "LogShifter" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new LogShifter(), manager) {
          (c) => new LogShifterTests(c)
        }
      },
      "VecSearch" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new VecSearch(), manager) {
          (c) => new VecSearchTests(c)
        }
      },
      "Stack" -> { (manager: TesterOptionsManager) =>
        Driver.execute(() => new Stack(8), manager) {
          (c) => new StackTests(c)
        }
      }
  )
  def main(args: Array[String]): Unit = {
    TutorialRunner("examples", examples, args)
  }
}
```

## Step 3: Learn rocket-chip [(Rocket Chip Generator)](https://github.com/chipsalliance/rocket-chip)

    1. How SBT build system work?
    2. Config system
    3. SoC TOP
    4. How to add custom SoC config?


## Step 4: Learn chipyard. [(Chipyard Framework)](https://github.com/ucb-bar/chipyard.git)

    1. Generators: Cores/Accelerators/Components
    2. Toolchains
    3. Software
    4. Simulator
    5. FPGA Prototyping
    6. Prototyping(Hammer)

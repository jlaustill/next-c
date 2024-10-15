# next-c
a thought exercise around what c/c++ would look like if I were to design it today, in 2024

## import/export

Every file in next-c is allowed to define only a single class, which is automatically exported.

To import the class from another file the syntax is

from "./location/of/my-class" import;

The name of the file MUST exactly match the name of the class. Classes must be Pascal cased, and the filename must be kebab case. This is to make sure it works with filesystems that aren't case sensitive(windows cough cough)

If you need to import two classes with the same name, you can assign a new name upon import as such

from "./src/my-class" import;
from "./lib/my-class" import LibMyClass;

And this will give you MyClass and LibMyClass

## variables

All variables are defined by size, no assumptions are EVER made, thus avoiding unsafe memory updates on 32/64 systems, etc. 

The syntax for defining a variable is

int8 aByte = 1;
float16 aFloat = 1.1;

variables can be nullable by using the nullable keyword

nullable int8 aNullableByte; // will be null

You can check for null by doing 

if (!aNullableByte) 
or
if (aNullableByte == null)

valid types are 

int8    uint8
int16   uint16
int32   uint32
int64   uint64

decimal8
decimal16
decimal32
decimal64
decimal128

string

## Basic Logic Syntax

All statements must end with a semi colon
Blocks don't require semi colons
Every class will default to static, if you need a data class, use the data keyword
Every class must be defined in a namespace, every libray should use a namespace that matches the libraries name.
Everything in a class will be private by default, use the public keyword to expose it publically. 

Example static class
from "./app-data.nc" import;
namespace Opcm {
    class Opcm {
        Opcm.AppData AppData = { vehicleSpeed: 0, engineRpm: 0 };

        int8 getVehicleSpeed() {
            return AppData.vehicleSpeed;
        }

        int8 setVehicleSpeed(int8 newSpeed) {
            AppData.vehicleSpeed = newSpeed;

            return getVehicleSpeed();
        }

    }
}

example data class
namespace Opcm {
    data class AppData {
        public nullable uint8 vehicleSpeed;

        public nullable uint16 engineRpm;
    }
}

### tabs vs spaces

simple, a tab is 4 spaces, so it doesn't matter

### Looping

basic for loop example

for (uint8 a = 0; a <= 128; a++) { // Same ++ -- as c/c++
    Console.log(`a is now ${a}`); // Same string interpolation as typescript
}

foreach loop example

foreach AppData.books as book, bookIndex { // All indexes are 1 based
    Console.log(`We have a book #${bookIndex} ${book}`); 
}

The same syntax applies for do and do/while loops
do {
    aThing();
} while (someVariable > 0);

while (someVariable > 0 ) {
    aThing();
}

### branching

basic if statement

int8 speed = 5;

if (speed == 5) { // double == is always equality, you can only check equality on the same types. You must explicitly cast to compare non like types
    doSomething();
} else {
    doSOmethingElse();
}

switch statement

switch speed {
    case 1: doSomething();
    case 2: case 3: case 4: // empty cases are automatically flowed threw, if a non empty case needs to flow through, use the continue word
    case > 6: logException(); continue; // case 5 will also execute
    case 5: doSOmethingElse();
    case mod 3 = 2: doEvenThing(); // example with mod
    default: doNothing();
}

case statements can use > < <= >= mod / and * 




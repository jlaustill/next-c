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



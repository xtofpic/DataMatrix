
# DataMatrix
Manage datamatrix code

The idea of this library is to have well defined functions signatures in library.
Instead of passing datamatrix code as a generic string in functions, you may pass only ai you need, and be sure ai is well formed.



Why there is no image parser.
Because the primary use of this library is to provide type to functions signatures.
My use case is to use a scanner device to retrieve GS1 codes.


# Usage
```c++
{
	...
	// Construct a gs1 code with only one gtin:
	gs1::code c;
	c.gtin = gs1::gtin { "55583421309548" };
	...
}

void aprintfunction(const gs1::code& c)
{
	std::cout << "passed code (hri formated): " << gs1::hri(c) << std::endl;
	std::cout << "passed code (binary formated): " << gs1::binary(c) << std::endl;
}

void aparsefunction(const std::string& s)	// s as binary formatted.
{
	gs1::code c;
	std::istringstream i(s);
	i >> gs1::binary(c, ']', '$');		// Will throw if s is not well formatted.
	std::cout << "The passed code (hri formatted): " << gs1::hri(c) << std::endl;
}

void anotherfunction(const gs1::gtin& gtin, const gs1::serial& serialNumber) // Enforce right signature.
{
	...
	gs1::code c;
	c.gtin = gtin;
	c.serial = serialNumber;
	std::cout << "code: " << gs1::hri(c) << std::endl;
	...
}

```



# How to compile:

Assert conan is installed on you system.
```
# pip install conan # or pip3 install conan
``̀ 

Create a build subdirectory.

In this subdirectory, launch cmake (for import in eclipse in the example below):
```
# cmake -G "Eclipse CDT4 - Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug -DCMAKE_ECLIPSE_GENERATE_SOURCE_PROJECT=TRUE -DCMAKE_ECLIPSE_MAKE_ARGUMENTS=-j12 -DCMAKE_ECLIPSE_VERSION=4.17 ..
# make
# env CTEST_OUTPUT_ON_FAILURE=1 make test
```



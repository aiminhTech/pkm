- Static Linking refers to the process of linking libraries to a program during its compilation phase, which essentially means that all the necessary library code needed for the program to run is included within the final executable binary.
- With static linking, each executable file operates independently of external
  libraries or shared objects.
- ## Advantages:
	- The program can be run on any system without the need of installing additional libraries, which makes it easier to distribute.
	- Since the libraries are built into the executable binary, the risk of encountering a library-related issue at runtime is reduced.
- ## Disadvantages:
	- The size of the executable file increases as all necessary code of the libraries is included in the final binary, which could lead to higher requirements for storage and memory.
	- Any changes to the library require the entire program to be re-linked and possibly re-compiled.
	- Multiple programs using the same library will each have their own copy of the library code, leading to increased disk space usage and reduced sharing at runtime.
- ## Note:
	- Static linking is different from dynamic linking, where the linking of
	  libraries is not done at compile time but at runtime. With dynamic linking,
	  multiple programs can share the same code from a library, which helps in saving
	  memory and allows updates to be made to the library without having to recompile
	  or relink the programs using it.
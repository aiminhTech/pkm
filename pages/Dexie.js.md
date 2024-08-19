tags:: [[JavaScript]], [[IndexedDB]]

- https://dexie.org/
- A popular library for working with IndexedDB, which is a client-side web database that allows you to store and manage structured data.
- ## Dexie in React
  collapsed:: true
	- https://dexie.org/docs/Tutorial/React
	- ### Installation
		- `npm install dexie`
		- `npm install dexie-react-hooks`
	- ### `db.ts`
		- ```typescript
		  export class AddressDatabase extends Dexie {
		    addresses!: Table<Address>;
		  
		    constructor() {
		      super("address");
		      this.version(1).stores({
		        addresses: "id, name, street, zip, city, phone, email",
		      });
		    }
		  }
		  
		  export const db = new AddressDatabase();
		  ```
		- **Class `AddressDatabase`**:
			- `export class AddressDatabase extends Dexie`: This line defines a class named `AddressDatabase` that extends the `Dexie` class. `Dexie` is
			- `addresses!: Table<Address>`: This line declares a property named `addresses` of type `Table<Address>`
			- `constructor() { ... }`: This is the class constructor that is executed when you create an instance of `AddressDatabase`.
	- ### Functions to add and remove some data
		- ```typescript
		  export async function addAddress(
		    address: Address,
		  ) {
		    try {
		      await db.addresses.add(address);
		    } catch (error) {
		      console.error(error);
		    }
		  }
		  
		  export async function removeAddress(
		    id: Id,
		  ) {
		    try {
		      await db.addresses.delete(id);
		    } catch (error) {
		      console.error(error);
		    }
		  }
		  ```
	- ### Read data
		- ```typescript
		  const addresses = useLiveQuery(
		      () => db.addresses.toArray()
		    )
		  ```
- ## Dexie in Angular
	- https://dexie.org/docs/Tutorial/Angular
	- TODO todo
-
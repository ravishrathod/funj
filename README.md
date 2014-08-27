funj
====

Collections and functional tools to complete the missing parts of Java/Guava.

To use with Maven:

	<dependency>
		<groupId>com.tek271</groupId>
		<artifactId>funj</artifactId>
		<version>1.0.0</version>
	</dependency>


Here is a list of some of the interesting parts:

CollectionTools
---------------

Let SomeEntity be a class with a property/field/getter named "id" of type long, and
a property "name" of type String.

	List<SomeEntity> entities = getEntities();
	Map<Long, SomeEntity> map = toMap(entities, "id");

Now the key in map is the id of SomeEntity, while the value is the SomeEntity object.

Now suppose you want to group entities by something which is not unique:

	Multimap<String, SomeEntity> toMultimap(entities, "name");


Finder
------
To find a list of objects with a matching property value:

	List<SomeEntity> foundList = findAll(entities, "id", 1, 2)

Will find entities whose id is either 1 or 2

	SomeEntity found = findFirst(entities, "name", "joe")

Will find the entity whose name property equals "joe"


Mapper
------
To extract/pluck a property from a list of entities:

	List<Long> ids = pluck(entities, "id");

To map the members of list using a callback function:

	List<Long> numbers = map(entities, this, "doubleTheId");

Assuming the ids where [1, 2, 3], numbers will have: [2, 4, 6].

The callback should be implemented as this:

	long doubleTheId(SomeEntity entity) {
		return entity.id * 2;
	}


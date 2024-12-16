# JSON
- Python allows you to use the popular data interchange format called JSON (JavaScript Object Notation). 
- The standard module called json can take Python data hierarchies, and convert them to string representations; this process is called serializing. 
- Reconstructing the data from the string representation is called deserializing. 
- Between serializing and deserializing, the string representing the object may have been stored in a file or data, or sent over a network connection to some distant machine.
- If you have an object x, you can view its JSON string representation with a simple line of code:
    ```
    import json
    x = [1, 'simple', 'list']
    json.dumps(x)       # '[1, "simple", "list"]'
    ```

- Another variant of the dumps() function, called dump(), simply serializes the object to a text file. So if f is a text file object opened for writing, we can do this:
    ```
    json.dump(x, f)     # where f is a text file opened for writing
    ```

- To decode the object again, if f is a binary file or text file object which has been opened for reading:
    ```
    x = json.load(f)    # loads json from a text or binary file and decodes the object
    ```

- JSON files must be encoded in UTF-8. Use encoding="utf-8" when opening JSON file as a text file for both of reading and writing.

- To make an object serializable either use JSONEncoder or toJSON method:
    ```
    import json
    from json import JSONEncoder

    class Car(dict):
        def __init__(self, make, model, year):
            super().__init__()
            self.make = make
            self.model = model
            self.year = year

        def __repr__(self):
            return f'<Car {self.make} {self.model} {self.year}>'

        def toJson(self):
            return json.dumps(self, default=lambda o: o.__dict__)

    class CarEncoder(JSONEncoder):
        def default(self, o):
            return o.__dict__

    car = Car('BMW', 'X5', 2024)

    print(car)

    print(CarEncoder().encode(car))

    carJSONData = json.dumps(car, indent=4, cls=CarEncoder)
    print(carJSONData)

    f = open('test2.txt', 'r+', encoding='utf-8')
    json.dump(CarEncoder().encode(car), f)

    carJSONData = json.dumps(car.toJson(), indent=4)
    print(carJSONData)

    print("Decode JSON formatted Data")
    carJSON = json.loads(carJSONData)
    print(carJSON)
    print(type(carJSON))

    carJSONData = json.dumps(car, indent=4)
    print(carJSONData)
    ```
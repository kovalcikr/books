# Item 12: Allways override toString

- it's recomended for all subclasses to override this method
- easier to debug
- should return all interesting information contained in object or summary
- specify format for value classes and provide way to convert
- provide programatic access to information contained in toString
- it makes no sense provide toString for utility class
- do not provide toString for enum types

´´´Python 
from math import atan2, degrees, pi

class Point:
    def __init__(self, x: float, y: float):
        self.__x = x
        self.__y = y

    def move(self, new_x, new_y):
        self.__x = new_x
        self.__y = new_y

    def get_x(self):
        return self.__x

    def get_y(self):
        return self.__y

    def set_x(self, x):
        self.__x = x

    def set_y(self, y):
        self.__y = y

class Line:
    def __init__(self, start, end):
        self.__start = start
        self.__end = end

    def compute_length(self):
        return ((self.__end.get_x() - self.__start.get_x()) ** 2 + (self.__end.get_y() - self.__start.get_y()) ** 2) ** 0.5

    def get_start(self):
        return self.__start

    def get_end(self):
        return self.__end

class Shape:
    def __init__(self, is_regular: bool):
        self.__is_regular = is_regular
        self.__vertices = []
        self.__edges = []
        self.__inner_angles = []

    def add_vertices(self, point):
        self.__vertices.append(point)

    def add_edges(self, line):
        self.__edges.append(line)

    def add_inner_angles(self, angles):
        self.__inner_angles = angles

    def compute_area(self):
        pass

    def compute_perimeter(self):
        pass

    def compute_inner_angles(self):
        pass

    def get_is_regular(self):
        return self.__is_regular

    def set_is_regular(self, is_regular):
        self.__is_regular = is_regular

    def get_vertices(self):
        return self.__vertices

    def get_edges(self):
        return self.__edges

    def get_inner_angles(self):
        return self.__inner_angles

class Rectangle(Shape):
    def __init__(self, width, height):
        super().__init__(is_regular=False)
        self.__width = width
        self.__height = height

    def compute_area(self):
        return self.__width * self.__height

    def compute_perimeter(self):
        return 2 * (self.__width + self.__height)

    def compute_inner_angles(self):
        if self.get_is_regular():
            return [90, 90, 90, 90]
        else:
            return None

    def get_width(self):
        return self.__width

    def set_width(self, width):
        self.__width = width

    def get_height(self):
        return self.__height

    def set_height(self, height):
        self.__height = height

class Square(Rectangle):
    def __init__(self, side_length):
        super().__init__(side_length, side_length)

class Triangle(Shape):
    def __init__(self, side1, side2, side3):
        super().__init__(is_regular=None)
        self.__side1 = side1
        self.__side2 = side2
        self.__side3 = side3

    def compute_area(self):
        s = (self.__side1 + self.__side2 + self.__side3) / 2
        return (s * (s - self.__side1) * (s - self.__side2) * (s - self.__side3)) ** 0.5

    def compute_perimeter(self):
        return self.__side1 + self.__side2 + self.__side3

    def compute_inner_angles(self):
        if len(self.get_inner_angles()) == 2:
            angle1, angle2 = self.get_inner_angles()
            angle3 = 180 - angle1 - angle2
            return [angle1, angle2, angle3]
        elif len(self.get_inner_angles()) == 1:
            angle1 = self.get_inner_angles()[0]
            angle2 = atan2(self.__height, self.__base) * 180 / pi
            angle3 = 180 - angle1 - angle2
            return [angle1, angle2, angle3]
        else:
            return None

    def get_side1(self):
        return self.__side1

    def set_side1(self, side1):
        self.__side1 = side1

    def get_side2(self):
        return self.__side2

    def set_side2(self, side2):
        self.__side2 = side2

    def get_side3(self):
        return self.__side3

    def set_side3(self, side3):
        self.__side3 = side3

class Isosceles(Triangle):
    def __init__(self):
        super().__init__(side1, side2, side3)

class Equilateral(Triangle):
    def __init__(self):
        super().__init__(side1, side2, side3)

class Scalene(Triangle):
    def __init__(self):
        super().__init__(side1, side2, side3)

class TriRectangle(Triangle):
    def __init__(self):
        super().__init__(side1, side2, side3)


# Create points
point1 = Point(0, 0)
point2 = Point(3, 0)
point3 = Point(3, 4)

# Create lines using points
line1 = Line(point1, point2)
line2 = Line(point2, point3)
line3 = Line(point3, point1)

# Create a rectangle with given lines
rectangle = Rectangle(line1.compute_length(), line2.compute_length())

# Calculate area and perimeter of the rectangle
area = rectangle.compute_area()
perimeter = rectangle.compute_perimeter()

# Output area and perimeter
print("Rectangle:")
print("Area:", area)
print("Perimeter:", perimeter)

# Create a triangle with given lines
triangle = Triangle(line1.compute_length(), line2.compute_length(), line3.compute_length())

# Calculate area and perimeter of the triangle
area = triangle.compute_area()
perimeter = triangle.compute_perimeter()

# Output area and perimeter
print("\nTriangle:")
print("Area:", area)
print("Perimeter:", perimeter)

# Set inner angles for the triangle
triangle.add_inner_angles([60, 60, 60])

# Calculate inner angles of the triangle
inner_angles = triangle.compute_inner_angles()

# Output inner angles
print("\nInner Angles of the Triangle:")
print(inner_angles)
´´´

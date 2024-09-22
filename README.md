# reto7
I Took the same code as reto3 and add a class called OrderIterator in wich I implemented the method __iter__ and __next__ and then because I'm gonna do the iteration in the class order I need also implement the method __iter__ and then return an object from orderIterator

`
class OrderIterator:
    def __init__(self, menu_items):
        self._menu_items = menu_items
        self._current_index = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self._current_index < len(self._menu_items):
            item = self._menu_items[self._current_index]
            self._current_index += 1
            return item
        else:
            raise StopIteration

class MenuItem:
    def __init__(self,name,price):
        self.name=name
        self.price=price
class Beverage(MenuItem):
    def __init__(self,name,price,volume,alcohol_content,lactose_free):
        super().__init__(name,price)
        self.volume=volume
        self.alcohol_content=alcohol_content
        self.lactose_free=lactose_free
    def set_volume(self,volume):
        self.volume=volume
    def set_alcohol_content(self,alcohol_content):
        self.alcohol_content=alcohol_content
    def set_lactose_free(self,lactose_free):
        self.lactose_free=lactose_free
    def get_volume(self):
        return self.volume 
    def get_alcohol_content(self):
        return self.alcohol_content
    def get_lactose_free(self):
        return self.lactose_free
        
class Appetizer(MenuItem):
    def __init__(self,name,price,calories):
        super().__init__(name,price)
        self.calories=calories
    def set_calories(self,calories):
        self.calories=calories
    def get_calories(self):
        return self.calories
    
class MainCourse(MenuItem):
    def __init__(self,name,price,calories,is_vegan):
        super().__init__(name,price)
        self.calories=calories
        self.is_vegan=is_vegan
    def set_calories(self,calories):
        self.calories=calories
    def set_is_vegan(self,is_vegan):
        self.is_vegan=is_vegan
    def get_calories(self):
        return self.calories
    def get_is_vegan(self):
        return self.is_vegan
    
class Dessert(MenuItem):
    def __init__(self,name,price,calories,is_gluten_free):
        super().__init__(name,price)
        self.calories=calories
        self.is_gluten_free=is_gluten_free
    def set_calories(self,calories):
        self.calories=calories
    def set_is_gluten_free(self,is_gluten_free):
        self.is_gluten_free=is_gluten_free
    def get_calories(self):
        return self.calories
    def get_is_gluten_free(self):
        return self.is_gluten_free

class Order:
    def __init__(self,table_number):
        self.table_number=table_number
        self.menu_items=[]
    def add_menu_item(self,menu_item):
        self.menu_items.append(menu_item)
    def is_main_course_included(self):
        for item in self.menu_items:
            if isinstance(item,MainCourse):
                return True
        return False
    
    def is_appetizer_included(self):
        for item in self.menu_items:
            if isinstance(item,Appetizer):
                return True
        return False
    def apply_discount(self):
        #is override according to the order composition
        if self.is_main_course_included():
            return (0.7,"Beverage")
        elif self.is_appetizer_included():
            return (0.8,"Dessert")
    def calculate_total_bill(self,discount):
        total=0
        for item in self.menu_items:
            if isinstance(item,Beverage) and (discount[1]=="Beverage"):
                total+=item.price*discount[0]
            elif isinstance(item,Dessert) and (discount[1]=="Dessert"):
                total+=item.price*discount[0]
            else:
                total+=item.price
        return total
    def get_items(self):
        items=[]
        for item in self.menu_items:
            items.append(item.name)
        return items
    def __iter__(self):
        return OrderIterator(self.menu_items)

order1=Order(1)
order1.add_menu_item(Appetizer("Nachos",10,300))
order1.add_menu_item(MainCourse("Pasta",20,500,False))
order1.add_menu_item(Dessert("Ice Cream",5,200,True))
order1.add_menu_item(Beverage("Beer",5,500,5,True))
order1.add_menu_item(Beverage("Water",2,500,0,True))
order1.add_menu_item(Appetizer("Guacamole",10,300))

for item in order1:
    print(item.name)
`


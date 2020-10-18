# Python parallel resistance

    #!/usr/bin/env python3
    
    # Python mumbo-jumbo for defining |?| as infix operator
    class Infix(object):
        def __init__(self, func):
            self.func = func
        def __ror__(self, x):
            return Infix(lambda y: self.func(x, y))
        def __or__(self, y):
            return self.func(y)
    
    # This creates the parallel-resistance operator as |P|
    P = Infix(lambda x, y: 1 / ((1 / x) + (1 / y)))
    
    
    #           R1   10
    #       .---\/\/\/\---.
    #       |             |    
    #       |   R2   15   |   R3   5
    #   o---+---\/\/\/\---+---\/\/\/\---+---o
    #       |                           |
    #       |     R4   5    R5   6      |
    #       '-----\/\/\/\---\/\/\/\-----'
    #   
    
    R1 = 10
    R2 = 15
    R3 = 5
    R4 = 5
    R5 = 6
    
    total = ((R1 |P| R2) + R3) |P| (R4 + R5)

    print(total)    # Output is: 5.5

    

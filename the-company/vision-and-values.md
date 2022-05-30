# Basic Contract Structure

## A example to use as a starting point

```python
"""
A hash is similar to a dict. If you try to read a none existing value, it will return the default_value.
Accessing multiple dimensions is not like a dict. You do data_store["first_dimension", "second_dimension"] instead of data_store["first_dimension"]["second_dimension"]
"""
data_store = Hash(default_value=0)

simple_store = Variable()

"""
The @construct annotation is used to declare a function that is run on deployment
"""
@construct
def seed():
    simple_store.set("simple string")
    data_store["first_dimension", "second_dimension"] = "data of second dimension"

"""
The @export annotation is used to declare a function that can be executed and is exposed to the public
"""    
@export
def a_function():
    user = ctx.caller # The caller of the function, can also be a contract if another contract executes this function
    transaction_signer = ctx.signer # You will get the user, even when the function is called from a contract
    this_contract = ctx.this # You will get the name of this contract
    return user # If this function is executed, it will have the address of the user returned

"""
If a @export function takes keyword arguments(kwargs), they will be available to be set by users
"""    
@export
def a_function_with_kwargs(a_string: str, a_integer: int, a_float: float, \
    a_list: list, a_dict: dict, a_datetime: datetime.datetime, \
    a_timedelta: datetime.timedelta, a_bool: bool):
    return a_string
    
"""
If a function has no annotation, it is only executable within the contract (no users)
"""
def another_function():
    pass

```

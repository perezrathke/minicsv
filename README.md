# minicsv

Bare minimal CSV stream based on C++ file streams where the stream operator can be overloaded for your custom type.

This is a example on how to write to CSV.

```cpp
#include "minicsv.h"

struct Product
{
    Product() : name(""), qty(0), price(0.0f) {}
    Product(std::string name_, int qty_, float price_) 
        : name(name_), qty(qty_), price(price_) {}
    std::string name;
    int qty;
    float price;
};

int main()
{
    csv::ofstream os("products.txt", std::ios_base::out);
    os.set_delimiter('\t');
    if(os.is_open())
    {
        Product product("Shampoo", 200, 15.0f);
        os << product.name << product.qty << product.price << NEWLINE;
        Product product2("Soap", 300, 6.0f);
        os << product2.name << product2.qty << product2.price << NEWLINE;
    }
    return 0;
}
```

This is a example on how to read from the same CSV.

```cpp
#include "minicsv.h"
#include <iostream>

int main()
{
    csv::ifstream is("products.txt", std::ios_base::in);
    is.set_delimiter('\t');
    if(is.is_open())
    {
        Product temp;
        while(!is.eof())
        {
            is >> temp.name >> temp.qty >> temp.price;
            // display the read items
            std::cout << temp.name << "," << temp.qty << "," << temp.price << std::endl;
        }
    }
    return 0;
}
```

The console output is shown below.

```
Shampoo,200,15
Soap,300,6
```

[CodeProject Tutorial](http://www.codeproject.com/Articles/741183/Minimalistic-CSV-Streams)
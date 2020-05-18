# Callback Method Inside a Class (C++)
``` C++
/*
 * =====================================================================================
 *
 *       Filename:  Test.cpp
 *
 *    Description:  :
 *
 *        Version:  1.0
 *        Created:  05/15/2020 08:20:28 AM
 *       Revision:  none
 *       Compiler:  gcc
 *
 *         Author:  YOUR NAME (), 
 *   Organization:  
 *
 * =====================================================================================
 */
#include <cstdio>

class Foo
{
public:
  Foo()
  {}

  void callbac(int count)
  {
    if (count > 10) return;
    printf("%d\n", count++);
  }

  void caller(void (Foo::*fnc)(int))
  {
    for (int i = 1; i < 12; ++i)
      (this->*fnc)(i);
  }

  void run()
  {
    caller(&Foo::callbac);
  }
};

int main()
{
  Foo foo;
  foo.run();
}
```

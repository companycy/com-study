# com-study


typedef struct {
  SetStringPtr * SetString;
  GetStringPtr * GetString;
} IExampleVtbl;

typedef struct {
  IExampleVtbl * lpVtbl;
  DWORD          count;
  char           buffer[80];
} IExample;


The other program is going to pass our IExample VTable GUID to our
QueryInterface() function, and we're going to check it to make sure it
is indeed the IExample VTable's GUID. If it is, then we'll return
something to let the program know that it indeed has an IExample
object.

The program calls our IClassFactory's CreateInstance whenever the
program wants us to create one of our IExample objects, initialize it,
and return it. The third argument will be the IExample VTable's GUID
(if someone indeed wants us to allocate, initialize, and return a
IExample object).

A program is going to call our DllGetClassObject to obtain a pointer
to our IClassFactory object. (Actually, as we'll see later, the
program is going to call an OLE function named CoGetClassObject, which
in turn calls our DllGetClassObject.) So, this is how the program gets
hold of our IClassFactory object -- by calling our DllGetClassObject.

http://www.codeproject.com/Articles/13601/COM-in-plain-C


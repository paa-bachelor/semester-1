# Numpy Guide
## METHODS

_np.pi_ returns pi

_np.sqrt(x)_ returns the square root of x

_np.roots(sequence1)_ returns an array of solutions to a polynomial which is defined by sequence1, where sequence1 is a sequence of descending coefficients of the polynomial

_np.loadtxt(file)_ returns an array with data from the given file, with optional arguments: _skiprows=int_ which skips the first _int_ rows before reading, default is 0. _delimiter=str1_ puts _str1_ between all data values, _unpack=Bool_ suppose the data has 3 values per datapoint ; if _unpack=True_ the method will return 3 seperate arrays consisting of each data point's first value, second value... default is False.

## ARRAYS
[**ARRAY CREATION**]

_np.array([sequence1],dtype=...)_ creates an array out of the elements of sequence 1, where dtype specifies the type of said elements

_np.linspace(a, b, c)_ returns an equally spaced array with lower- and upper limit a and b containing c(optional, default is 50) elements  

_np.arange(a, b, c)_ returns an equally spaced array with lower- and upper limit a and b(b not in array) with step size c(optional, default is 1)

_X,Y = np.meshgrid(array1,array2)_ returns a 2 arrays X and Y, where X is array1 extended in the y-direction and Y is array2 extended in the x-direction

_np.zeros(tuple1)_ returns an array of zeroes with the shape of tuple1

_np.ones(tuple1)_ returns an array of ones with the shape of tuple1

_np.identity(x)_ returns an array of ones with the shape (x,x)

_np.full(tuple1,x)_ returns an array of x with the shape of tuple1

_np.exp(array1)_ returns an array where the elements are the exponential function evaluated in the elements of array1

[**ARRAY INFORMATION**]

_array1.dtype_ returns the type of the elements of array1

_array1.ndim_ returns the dimension of array1 (0 = scalar, 1= vector, 2= matrix..)

_np.shape(array1)_ returns a tuple containing the shape of array1

[**ARRAY TINKERING**]

_array1.reshape(tuple1)_ returns array1 as an array with the shape given by tuple1

_array1.T_ returns the transpose of array1(columns and rows have been swapped)

_np.split(array1,x)_ returns a list of x(int) arrays, where array1 has been splitted up into said arrays(only works if len(array1)|x)

## INDEXING

[**ONE-DIMENSIONAL INDEXING**]

Suppose array1 is an array containing ndarrays, array[:,x] will return an array of the xth element of each ndarray in array1

[**N-DIMENSIONAL INDEXING**]




[**BOOLEAN INDEXING**]




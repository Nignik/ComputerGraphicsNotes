### gcd
```cpp
int gcd (int a, int b) { 
if (b == 0) 
	return a;
else 
	return gcd (b, a % b); }
```

### primes
```python
def is_prime(x):
    if x <= 1:
        return False
    for i in range(2, int(x**0.5) + 1):
        if x % i == 0:
            return False
    return True
```

```python
def get_prime(n):  
    is_prime = [1] * (n+1)  
    is_prime[0] = 0  
    is_prime[1] = 0  
  
    i = 2  
    while i*i <= n:  
        if is_prime[i]:  
            for j in range(i*i, n+1, i):  
                is_prime[j] = 0  
        i += 1  
    return is_prime
```

```python
def prime_factors(n):
    k = 2
    while n != 1:
        while n % k == 0:
            n //= k
            print(k)  # albo do tablicy sobie wrzucać
        k += 1
```

### zachłanna reszta
```python
do_wydania = 6
monety = [1, 2, 5]

def wydawanie(do_wydania, monety):
    count = 0
    historia = []

    while do_wydania > 0:
        nominal = 0
        for i in range(len(monety)):
            if do_wydania >= monety[i] > nominal:
                nominal = monety[i]
        do_wydania -= nominal

        historia.append(nominal)
        count += 1

    return f'Reszte wydasz w {count} monetach, te monety to {historia}'

print(wydawanie(do_wydania, monety))
```

### fast exp
```python
def fast_power(base, power):
    result, m = 1, 1000000007
    while power > 0:
        if power % 2 == 1:
            result = (result * base) % m
        power //= 2
        base = (base * base) % m
    return result
```

### bisekcja
```python
def f(x):
    return -4 * x + 2

# bisection(od,do)
def bisection(a, b, precyzja=0.0001):
    if f(a) * f(b) >= 0:
        return None
    c = a
    while b - a >= precyzja:
        c = (a + b) / 2
        if f(c) == 0.0:
            break
        if f(c) * f(a) < 0:
            b = c
        else:
            a = c
    return c
```

### square root approximation
```cpp
double sqrt_newton(double n) { 
	const double eps = 1E-15; 
	double x = 1; 
	for (;;) { 
		double nx = (x + n / x) / 2; 
		if (abs(x - nx) < eps)
			break; x = nx; 
	}
	return x; 
}
```

### horners method
```python
def horner_eval(coeffs, x):
    """
    Evaluate a polynomial at x using Horner’s method.

    Parameters
    ----------
    coeffs : list or tuple
        Polynomial coefficients ordered from highest power to constant term.
        For p(x) = a_n x^n + a_{n-1} x^{n-1} + ... + a_1 x + a_0,
        pass coeffs = [a_n, a_{n-1}, …, a_1, a_0].
    x : int | float
        Point at which to evaluate p(x).

    Returns
    -------
    value : same type as x
        The polynomial value p(x).
    """
    result = 0
    for a in coeffs:           # iterate from highest degree down
        result = result * x + a
    return result
```

### finding roots
```python
def func(x):
    return x*x*x - x*x + 2
 
# Prints root of func(x)
# with error of EPSILON
def bisection(a,b):

    if (func(a) * func(b) >= 0):
        print("You have not assumed right a and b\n")
        return
       c = a
    while ((b-a) >= 0.01):

        # Find middle point
        c = (a+b)/2
 
        # Check if middle point is root
        if (func(c) == 0.0):
            break
 
        # Decide the side to repeat the steps
        if (func(c)*func(a) < 0):
            b = c
        else:
            a = c     
    print("The value of root is : ","%.4f"%c)
    
# Driver code
# Initial values assumed
a =-200
b = 300
bisection(a, b)
```

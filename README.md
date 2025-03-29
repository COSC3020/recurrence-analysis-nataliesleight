# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```


Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.


The recurrence relation is $3T(n/3) + n^5$ for $n > 1$ where for $n ≤ 1$, $T(1) = 1$.

This is because when $n ≤ 1$ the funtcion performs a check and returns. For any other value of $n$, the function makes 3 recursive called with argument $n/3$ and goes through 
a for loop that adds $(n* n) * (n) * (n*n) = n^5$ to the funciton.

$T(n) = 3T(\frac{n}{3}) + n^5$

$= 3(3T(\frac{\frac{n}{3}}{3}) + (\frac{n}{3})^5) + n^5$

$= 3^2 T(\frac{n}{3^2}) + 3\frac{n}{3})^5 + n^5$

$= 3^2(3 T(\frac{\frac{n}{3^2}}{3}) + (\frac{n}{3^2})^5)) + 3\frac{n}{3})^5 + n^5$

$= 3^3 T(\frac{n}{3^3}) + 3^2\frac{n}{3^2}^5 + 3\frac{n}{3})^5 + n^5$

$= 3^3(3 T(\frac{\frac{n}{3^3}{3}) + (\frac{n}{3^3})^5)) + 3^2\frac{n}{3^2}^5 + 3\frac{n}{3})^5 + n^5$

$= 3^4 T(\frac{n}{3^4}) + 3^3\frac{n}{3^3}^5 + 3^2\frac{n}{3^2}^5 + 3\frac{n}{3})^5 + n^5$

$= 3^4 T(\frac{n}{3^4}) + \frac{3^3}{3^15}n^5 + \frac{3^2}{3^10}n^5 + \frac{3}{3^5}n^5 + n^5$

$= 3^4 T(\frac{n}{3^4}) + 3^{-12}n^5 + 3^{-8}n^5 + 3^{-4}n^5 + 3^0n^5$

$= 3^i T(\frac{n}{3^i}) + n^5 \sum_{k=0}^{i-1}(3^{-4})^k$
    
for $i = \log{_3}{n}$

$= 3^{\log{3}{n}} T(\frac{n}{3^\log{3}{n}}) + n^5 \sum_{k=0}^{\log{_3}{n}-1}(3^{-4})^k$

by geometric series sum

$= nT(1) + n^5 (\frac{1-(3^{-4})^{\log{_3-1}{n}}}{1-3^{-4}}$

$= n + n^5 (\frac{81}{80} - \frac{3^8}{80n^4})$

$= n + \frac{81}{80}n^5 - \frac{3^8}{80}n$

$= \frac{81}{80}n^5 - \frac{80-3^8}{80}n$

$T(n) ∈ Θ(\frac{81}{80}n^5)$

### Sources: I received help from Lars Kothoff.

I used this link to help guide my recurrecne math: https://tildesites.bowdoin.edu/~ltoma/teaching/cs231/fall14/Lectures/02-recurrences/recurrences.pdf 

“I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.” - Natalie Sleight 


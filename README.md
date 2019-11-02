#include <stdio.h>
int arithResult(int CreditNumArr[], int sum, int count);
int main ()

{
    long creditnumber;
    int count = 0;
    long ten = 1;
    printf("Enter credit card number     ");
    scanf("%ld", &creditnumber);
    long creditnumber2 = creditnumber;  // copy value to the despensable creditnumber2
    
    while (creditnumber2 != 0) //creditnumber2 being destroyed.
        // count number of digits.
    {
        creditnumber2 /=10;
        count++;
        ten *=10; //get the divisor for the Array.
    } 
    
    long checkcardtype = ten / 100; //copy ten value into cardtype
    ten /=10; //remove 1 zero.
    int CreditNumArr[count]; 
    
    for (int i = 0; count > i; i++)//get every value for the array
    {
        CreditNumArr[i] = creditnumber / ten % 10;
        ten /=10;    
    }
    int sum = 0; //perform arithmetic
    sum = arithResult(CreditNumArr, sum, count);
    if (sum % 10 == 0)
    {     
        long firsttwodigits;
        firsttwodigits = creditnumber / checkcardtype;
        if (firsttwodigits == 51 || firsttwodigits == 52 || firsttwodigits == 53 || firsttwodigits == 54 || firsttwodigits == 55 ||             firsttwodigits == 22)
        {
            printf("MASTERCARD\n");
        }
        else if (firsttwodigits/10 == 4)
        {
            printf("VISA\n");
        }
        else if (firsttwodigits == 34 || firsttwodigits == 37)
        {
            printf("AMEX\n");
        }
        else
        {
            printf("Your card is not AMEX, Mastercard, nor Visa.");
        }
    }
    else
    {
         //printf("\nsum before mod = %d", sum);
        printf("INVALID"); 
    }
    return 0;
}

int arithResult(int CreditNumArr[], int sum, int count)
{
    int productdigits[count];
    int digitmod;
    int digitdiv;
    
    for (int i = count - 2; i >= 0; i -=2) 
    {   
       // printf("\ni value: %d\n", i);
        productdigits[i] = CreditNumArr[i]*2;
        if (productdigits[i] >= 10)
        {   
            //printf("\ndigit%d = %d\n", i, productdigits[i]);
            digitmod = productdigits[i] % 10;
            digitdiv = productdigits[i] / 10;
            sum += digitmod + digitdiv;
        }
      
        else 
        {
             sum += productdigits[i];
            // printf("\ndigit%d = %d\n", i, productdigits[i]);
        }
    }
    
    for (int y = count - 1; y >= 0; y -=2)
    {
        sum += CreditNumArr[y];
    }
    return sum;
}


/**
* @author Nia Jacobs, 2002559351, Assignment 8
* @brief This implementation is a calculator for polynomials. it utilizes
a linked list to perform this math (each node keeps the coefficient value and a pointer to the next node)
 Since the main program coefficient arrays run smallest to biggest degree,
 I initially flip the array pattern since I made the program
 with the biggest degree first in mind. Ultimately, this assignment
 is a polynomial calculator that emphasizes the topics linked list and 
 operator overload. 
* Academic Integrity Policy while completing this assignment.
* @note implementation og polynomial.h
*/
#include "polynomial.h"
#include <iostream>
#include <cstdlib>
#include <cmath>
using namespace std;

//default constructor
polynomial::polynomial() 
{
	degree = -1;
    head = nullptr;

}
	
//deep-copy constructor
polynomial::polynomial(const polynomial& poly)
{
   //setting degree the same
	this->degree = poly.degree;
    
    //checking if linked list even has anything
    if (poly.head == nullptr)
    {
        head = nullptr;
    }
    else //good to go
    {
        //making pointers to traverse list
        node* cur = poly.head;
        node* tail = nullptr; //end
        this->head = nullptr; //front

        while(cur != nullptr)
        {
            //copying other polynomials node
            node* next = new node;
            next->coefficient = cur->coefficient;
            next->link = nullptr;

            
            if (this->head == nullptr) //first run to set head
            {
                this->head = next;
                //delete next;
                tail = next;
            }
            else //the rest of the list
            {
                tail->link = next;
                tail = next;
            }
            cur = cur->link; //moving on to next node in other polynomial
        
        }
    }

    
    
}

//construcot that sets polynomial to just an integer	
polynomial::polynomial(int s)
{
	degree = 0; // x^0 = 1

    head = new node;
    head->coefficient = s;
    head->link = nullptr;
}

//deconstructor
polynomial::~polynomial()
{
    
	node *temp; //created temp save pointer
    while (head != nullptr)
    {
        temp = head; //shallow copy so points to the same
        head = head->link;
        delete temp;
    }
    


    
   
    
}

//constructor takes array of coefficients, flips it and takes degree
polynomial::polynomial(int p[], int degree)
{
    //cout << "ayy";
    head = nullptr;
	this->degree = degree;
    node *tail = nullptr;

    //flipping array so its intuitive for me lol(big degree first)
    for (int j = 0; j < degree; j++)
    {
    for (int i = 0; i < degree - j; i++)
    {
        int save = p[i];
        p[i] = p[i + 1];
        p[i + 1] = save;
    }
    }
    
    //creating polynomial
    for (int i = 0; i <= degree; i++)
    {
        node *next = new node; //allocate to heap each node
        next->coefficient = p[i];
        //cout << "ayy";
        next->link = nullptr;
    

    if (head == nullptr) // create head
    {
        
        head = next;
        tail = next;
    }
    else //making the rest of list
    {
        tail->link = next;
        tail = next;
    }
    }

    /* my first try, realized i needed pointer to traverse
    int count = 0;
    while (p != nullptr)
    {
        /*
        node* linknode = new node();
        linknode->coefficient = p[count + 1];
        next->link = linknode;
        node* next = new node();
        linknode->link = next;
        next->coefficient = p[count + 2];
        next->link = nullptr;
        count++;
        
        
        
    }
        */
    

}
	

//polynomial operator overload for multipication, multiplies a poynomial with another polynomial
polynomial polynomial::operator*(const polynomial& rhs) const
{

    //checking pointing
	if (this->degree < 0 || rhs.degree < 0)
    {
        return polynomial();
    }


    int newdegree = this->degree + rhs.degree;//creating the new degree by adding (mult powers = adding)
    int* tcoe = new int[newdegree + 1]; //stands for (t)his (coe)fficient, a dynamic array to store coefficients

    //default vals 
    for (int i = 0; i <= newdegree; i++)
    {
        tcoe[i] = 0;
    }

    node* first = this->head; //pnter to traverse
    int i = 0;
    while (first != nullptr)
    {
        node* second = rhs.head;
        int j = 0;
        while (second != nullptr) //multiplying  1 val by each value of other
        {
            tcoe[i + j] += first->coefficient * second->coefficient;

            second = second->link;
            j++;
        }
        first = first->link; //going over to next val
        i++;
    }

    
    //flipping array, so higher degree coefs are closer to head
    for (int j = 0; j < newdegree; j++)
    {
        for (int i = 0; i < newdegree - j; i++)
        {
            int save = tcoe[i];
            tcoe[i] = tcoe[i + 1];
            tcoe[i + 1] = save;
        }
    }
    

    polynomial product(tcoe, newdegree); //making polynomial using coefficients

    polynomial final(product); //made deep copy, cus some reason itd giver error when i deleted tcoe without this

    

    //cout << "yippee" << endl;
    delete[] tcoe;

    return final;
}

//polynomial operator overload for multiplying a polynomial with an integer
polynomial polynomial::operator*(int rhs) const
{
 
    polynomial product(*this); //creating deep copy

    node* curr = product.head; //pointer to traverse
    //curr = product.head;

    while(curr != nullptr)
    {
        curr->coefficient *= rhs; //multiplying each coef b the integer
        //cout << curr->coefficient << endl;
        curr = curr->link;
    }

    return product;
    
}


polynomial polynomial::operator+(const polynomial& rhs) const
{
   
   polynomial sum;
   int degreedif; //degree difference
   bool thisgreater = false;

   //seeing which poly is greater 
    if (degree > rhs.degree)
    {
        //polynomial sum(*this);
        sum = *this;
        //cout << (head->coefficient == sum.head->coefficient) << endl;
        degreedif = degree - rhs.degree;
        thisgreater = true;
        //cout << degreedif << endl;
        

    }
    else
    {
    
        //polynomial sum(rhs);
        sum = rhs;
        degreedif = rhs.degree - degree;
        //cout << degreedif << endl;
    }

    //pointers to traverse each polynomial
    node* curr = sum.head;
    node* thisnode = head;
    node* other = rhs.head;
    int degreecnt = 0;

    while (curr != nullptr)
    {
        //cout << "here" << endl;
        if (degreecnt < degreedif) //so if one if larger, the larger will keep the difference of their degrees
        {
            if (thisgreater == true)
            {
                thisnode = thisnode->link;
                curr = curr->link;
                degreecnt++;
            }
            else
            {
                other = other->link;
                curr = curr->link;
                degreecnt++;
            }
            continue;
        }

        
        //cout << "after" << endl;

        curr->coefficient = thisnode->coefficient + other->coefficient;
        //cout << "1" << endl;
        curr = curr->link;
        //cout << "2" << endl;
        thisnode = thisnode->link;
        //cout << "3" << endl;
        other = other->link;

    
    }

    return sum;

}


//operation overload for +, adding a polynomial to an integer
polynomial polynomial::operator+(int rhs) const
{
    polynomial sum(*this);
    node* cur = sum.head;
	for (int i = 0; i <=degree; i++)
    {
        
        if (i == degree)
        {
            cur->coefficient += rhs; //adding to last val
            cur->link = nullptr;
            return sum;
        }
        cur = cur->link;
    }

    return sum;
}

//overload for = operator, sets poly = to other poly
const polynomial& polynomial::operator=(const polynomial& rhs)
{

    //copied the deep copy constructor but made adjustments so it returns *this 
	this->degree = rhs.degree;

    node *temp; //created temp save pointer
    while (head != nullptr)
    {
        temp = head; //shallow copy so points to the same
        head = head->link;
        delete temp;
    }
    head = nullptr;
    
    if (rhs.head == nullptr)
    {
        head = nullptr;
    }
    else
    {
        node* cur = rhs.head;
        node* tail = nullptr;
        this->head = nullptr;

        while(cur != nullptr)
        {
            node* next = new node;
            next->coefficient = cur->coefficient;
            next->link = nullptr;

            if (this->head == nullptr)
            {
                this->head = next;
                tail = next;
            }
            else
            {
                tail->link = next;
                tail = next;
            }
            cur = cur->link;
        
        }
    }

    return *this;

}

//overloaded = operator to make poly an int.
const polynomial& polynomial::operator=(int rhs)
{

    //getting rid of current polynomial
    node* save;
    while (head != nullptr)
    {
        save = head;
        head = head->link;
        delete save;
    }

    degree = 0;

    //setting polynomial
    head = new node;
    head->coefficient = rhs;
    head->link = nullptr;
    polynomial integer(rhs);
    

    return *this;
}

//make polynomial opposite sign
polynomial polynomial::operator-() const
{
	polynomial product(*this);

    node* curr = product.head;
    //curr = product.head;

    while(curr != nullptr)
    {
        curr->coefficient *= -1; 
        curr = curr->link;
    }

    return product;
}

//overloaded -, makes it so u subtract a polynomial from a polynomial
polynomial polynomial::operator-(const polynomial& rhs) const
{
	polynomial difference;
   int degreedif;
    bool thisgreater = false;

    if (degree > rhs.degree)
    {
        //polynomial sum(*this);
        difference = *this;
        //cout << (head->coefficient == sum.head->coefficient) << endl;
        degreedif = degree - rhs.degree;
        thisgreater = true;
        //cout << degreedif << endl;
        

    }
    else
    {
    
        //polynomial sum(rhs);
        difference = rhs;
        degreedif = rhs.degree - degree;
        //cout << degreedif << endl;
    }

    node* curr = difference.head;
    node* thisnode = head;
    node* other = rhs.head;
    int degreecnt = 0;

    while (curr != nullptr)
    {
        //cout << "here" << endl;
        if (degreecnt < degreedif)
        {
            if (thisgreater == true)
            {
                thisnode = thisnode->link;
                curr = curr->link;
                degreecnt++;
            }
            else
            {
                other = other->link;
                curr->coefficient *= -1;
                curr = curr->link;
                degreecnt++;
            }
            continue;
        }

        
        //cout << "after" << endl;

        curr->coefficient = thisnode->coefficient - other->coefficient;
        //cout << "1" << endl;
        curr = curr->link;
        //cout << "2" << endl;
        thisnode = thisnode->link;
        //cout << "3" << endl;
        other = other->link;

    
    }

    return difference;
}


//- overload for subtracted an int from a polynomial
polynomial polynomial::operator-(int rhs) const
{
    polynomial difference(*this);
    node* cur = difference.head;
	for (int i = 0; i <=degree; i++)
    {
        
        if (i == degree)
        {
            cur->coefficient -= rhs; //subtracting from final val
        }
        cur = cur->link;
    }

    return difference;
}

//friend func overload for << prints out the polynomial in its usual form
ostream& operator<<(ostream& outfile, const polynomial& rhs)
{
    
    polynomial::node* cnt = rhs.head;
    bool first = true;
    for (int i = 0; i <= rhs.degree ; i++)
    {
        //cout << "hii" << endl;
        if (cnt->coefficient == 0)
        {
            //cout << "yipee" << endl;
            cnt = cnt->link;
            continue;
        }
        if (first == true) // the sign will be attatched if its the highest degree
        {
            if ((rhs.degree - i) == 1 ) //not degree just x shown
            {
                if (cnt->coefficient == 1) //these if statements are all around to check if i need to sacrafice the 1 and make it just x
                {
                    cout << "x";
                }
                else if(cnt->coefficient == -1)
                {
                    cout << "-x";
                }
                else
                {
                cout << cnt->coefficient << "x";
                }
            }
            else if ((rhs.degree - i) == 0 )
            {
                cout << cnt->coefficient;
            }
            else
            {
                if (cnt->coefficient == 1)
                {
                    cout << "x^" << rhs.degree - i;
                }
                else if(cnt->coefficient == -1)
                {
                    cout << "-x^" << rhs.degree - i;
                }
                else
                {
                cout << cnt->coefficient << "x^" << rhs.degree - i;
                }
            }
            first = false;
            cnt = cnt->link;
            continue;
        }


        if(cnt->coefficient < 0) //if negative
        {
            if (cnt->coefficient != -1) //anything except -1 if its -1 it disregards a coef number
            {
                if ((rhs.degree - i) == 1)
                {
                    cout << " - " << -cnt->coefficient << "x";
                }
                else if ((rhs.degree - i) == 0)
                {
                    cout << " - " << -cnt->coefficient;
                }
                else
                {
                    cout << " - " << -cnt->coefficient << "x^" << rhs.degree - i;
                }
            }
            else if (cnt->coefficient == -1)
            {
                if ((rhs.degree - i) == 1)
                {
                    cout << " - " <<  "x";
                }
                else if ((rhs.degree - i) == 0)
                {
                    cout << " - " << -cnt->coefficient;
                }
                else
                {
                    cout << " - " << "x^" << rhs.degree - i;
                }
            }
        }
        else //if positive
        {
            if (cnt->coefficient != 1)
            {
                if ((rhs.degree - i) == 1)
                {
                    cout << " + " << cnt->coefficient << "x";
                }
                else if ((rhs.degree - i) == 0)
                {
                    cout << " + " << cnt->coefficient;
                }
                else
                {
                    cout << " + " << cnt->coefficient << "x^" << rhs.degree - i;
                }
            }
            else
            {
                if ((rhs.degree - i) == 1)
                {
                    cout << " + " << "x";
                }
                else if ((rhs.degree - i) == 0)
                {
                    cout << " + " << cnt->coefficient;
                }
                else
                {
                    cout << " + " <<  "x^" << rhs.degree - i;
                }
            }
        }

        cnt = cnt->link;
        
    }	

    return cout;
    }

//friend func that overloads + to add a number to a polynomial
polynomial operator+(int lhs, const polynomial& rhs)
{
	return rhs + lhs; //using earlier member so u can add the other way
}

//friend func that overloads *, multiplies a polynomial with an integer
polynomial operator*(int lhs, const polynomial& rhs)
{
    return rhs * lhs; //use earlier member
}

//friend func for -, subtracts a polynomial from an integer
polynomial operator-(int lhs, const polynomial& rhs)
{
    //cant use past member since its a lil difference
	polynomial difference(rhs);
    polynomial::node* cur = difference.head;
	for (int i = 0; i <= rhs.degree; i++)
    {  
        if (i == rhs.degree)
        {
            cur->coefficient = lhs - cur->coefficient; // subtracting from last val
        }
        else
        {
            cur->coefficient = -cur->coefficient; //changes slides
        }
        cur = cur->link;
    }

    return difference;
}

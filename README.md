# chain_of_responsibility_ATM

#include<iostream>
using namespace std;

#define CASH_DISPENSE 1
#define INVALID_REQ 0

#define BILL_100  100
#define BILL_200  200
#define BILL_500   500
#define BILL_2000   2000

class ATMModule
{

protected:
int m_nReqType;
ATMModule* pNext;

public:
ATMModule(int nReqType)
{
m_nReqType = nReqtype;
}

void SetNextSlot(ATMModule* pNext)
{
  this->pNext = pNext;                                             // here this one is setting the next handler
}

virtual int Run(int nCurrency)
{

return INVALID_REQ;                                   // performing task of dispensing the cash depending on what kind of request we have placed..
}

};


class Slot_100 : public ATMModule
{
public:
    Slot_100():ATMModule(BILL_100)
{
pNext = NULL;                                             // by default next handler will be set to NULL
}

Virtual int Run(int nCurrency)
{
  if (m_nReqType == nCurrency)
      {
       cout<<endl<<"in right slot";
       return CASH_DISPENSE;
      }

  else
     {
       if(pNext == NULL)
         {
             cout<<"not available"<<endl;
             return INVALID_REQ;
         }    
   
      cout<<endl<<"Moving to next slot";
      return pNext->Run(nCurrency);
     }
}  
};

class Slot_200 : public ATMModule
{
public:
    Slot_200():ATMModule(BILL_200)
{
pNext = NULL;                                             // by default next handler will be set to NULL
}

Virtual int Run(int nCurrency)
{
  if (m_nReqType == nCurrency)
      {
       cout<<endl<<"in right slot";
       return CASH_DISPENSE;
      }

  else
     {
        if(pNext == NULL)
         {
             cout<<"not available"<<endl;
             return INVALID_REQ;
         }    
      
      cout<<endl<<"Moving to next slot";
      return pNext->Run(nCurrency);
     }
}  
};


class Slot_500 : public ATMModule
{
public:
    Slot_500():ATMModule(BILL_500)
{
pNext = NULL;                                             // by default next handler will be set to NULL
}

Virtual int Run(int nCurrency)
{
  if (m_nReqType == nCurrency)
      {
       cout<<endl<<"in right slot";
       return CASH_DISPENSE;
      }

  else
     {
        if(pNext == NULL)
         {
             cout<<"not available"<<endl;
             return INVALID_REQ;
         }    

      cout<<endl<<"Moving to next slot";
      return pNext->Run(nCurrency);
     }
}  
};

class Slot_2000 : public ATMModule
{
public:
    Slot_2000():ATMModule(BILL_2000)
{
pNext = NULL;                                             // by default next handler will be set to NULL
}

Virtual int Run(int nCurrency)
{
  if (m_nReqType == nCurrency)
      {
       cout<<endl<<"in right slot";
       return CASH_DISPENSE;
      }

  else
     {
        if(pNext == NULL)
         {
             cout<<"not available"<<endl;
             return INVALID_REQ;
         }    
      
      cout<<endl<<"Moving to next slot";
      return pNext->Run(nCurrency);
     }
}  
};

int main()
{
ATMModule* p1 = new Slot_100();
ATMModule* p2 = new Slot_200();
ATMModule* p3 = new Slot_500();
ATMModule* p4 = new Slot_2000();

p1->SetNextSlot(p2);
p2->SetNextSlot(p3);
p3->SetNextSlot(p4);

p1->Run(500);
return 0;
}

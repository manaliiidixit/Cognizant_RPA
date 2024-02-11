# Cognizant_RPA


Maddoffs Minions:

using System;
using System.Collections.Generic; 
using System.Linq; using System.Collections; 
public class Program  
{  

    public static Dictionary<string,float> empDictionary=new Dictionary<string,float>();
    public static void Main(string[] args)  

    {  

        empDictionary.Add("EMP101",2.5f);   
        empDictionary.Add("EMP102",4.3f); 
        empDictionary.Add("EMP103",5.0f); 
        empDictionary.Add("EMP104",3.4f); 
        empDictionary.Add("EMP105",6.0f); 
        Program pr=new Program();     
        while(true)  

        {  

            Console.WriteLine("Enter your choice");  

            Console.WriteLine("1. Find Employee Rating\n2. Find Employee With Highest Rating\n3. Sort Employees By Rating\n4. Exit");     
            int choice=int.Parse(Console.ReadLine());          
            switch(choice)  

            {        
                case 1:  

                    Console.WriteLine("Enter the employee id"); 
                    string k=Console.ReadLine();     
                    float res=pr.FindEmployeeRating(k);  

                    if(res==-1)  

                    {  

                        Console.WriteLine("Invalid employee id");  

                    }     
                    else  

                    {  

                        Console.WriteLine("Rating is : "+res);  

                    }     
                    break;
                    case 2:  

                        Console.WriteLine("Enter the Rating");     
                        float rating=float.Parse(Console.ReadLine());  

                        List<string> list=pr.FindEmployeeWithHighestRating(rating);  

                        if(list.Count>0)  

                        {  

                            foreach(string item in list)  

                            {  

                                Console.WriteLine(item);  

                            }              
                            }              
                            else  

                        {  

                            Console.WriteLine("No highest rating employees found");  

                        }  

                        break;    
                        case 3:  

                        Dictionary<string,float> mydict=pr.SortByRating();    
                        Console.WriteLine("EmployeeId\tRating");       
                        foreach(var item in mydict)  

                        {  

                            Console.WriteLine($"{item.Key}\t\t{item.Value}");  

                        }                   
                        break;             
                        case 4:  

                        Console.WriteLine("Thank you");  

                        return;  

            }  

              

        }  

          

    }  

    public float FindEmployeeRating(string empid)  

    {  

        float res1=-1;  

        foreach(var item in empDictionary)  

        {  

            if(item.Key==empid)  

            {  

                res1=item.Value;  

            }  

        }  

        return res1;  

  

    }  

    public List<string> FindEmployeeWithHighestRating(float rating)  

    {  

        List<string> k=new List<string>();
        foreach(var item in empDictionary)  

        {  

            if(rating==item.Value)  

            {  

                k.Add(item.Key);  

            }  

        }  

        return k;  

    }  

    public Dictionary<string,float> SortByRating()  

    {  

        return empDictionary.OrderByDescending(c=>c.Value).ToDictionary(a=>a.Key,a=>a.Value);  

    }  

  

}







Retired hub:

using System;
class  Club{
  
  public string MemberId{get; set;}
  public string MemberName{get; set;}
  public string MemberType{get;set;}
}

class Service : Club{
    
    public bool ValidateMemberId(){
        if(MemberId.Contains("Gold"))
        {
            int i=0;
            string temp = MemberId.Substring(4);
            if(temp.Length !=4)//this is to check that there should only be 4 digits
           {
               return false;
           }
            
            if(int.TryParse(temp,out i))//this is to check if all four digits are numbers
            {
                return true;
            }
            else{
                return false;
            }
        }
        else if(MemberId.Contains("Premium"))
        {
            int i =0;
           string temp = MemberId.Substring(7); 
           if(temp.Length !=4)//this is to check that there should only be 4 digits
           {
               return false;
           }
           
           if(int.TryParse(temp,out i))//this is to check if all four digits are numbers
            {
                return true;
            }
            else{
                return false;
            }
        }
        return false;
    }
    public double CalculateMemberFees()
    {
        if(MemberType.Equals("Gold"))
        {
            return 50000;
        }
        else if(MemberType.Equals("Premium"))
        {
            return 75000;
        }
        return 0;
    }
}




public class Program{

    static void Main(){
        Service obj = new Service();
        Console.WriteLine("Enter Member Id:");
        string memid = Console.ReadLine();
        obj.MemberId = memid;
        bool res= obj.ValidateMemberId();
        if(res == true)
        {
            Console.WriteLine("Enter Member Name:");
            string memname = Console.ReadLine();
            Console.WriteLine("Enter Member Type:");
            string memtype = Console.ReadLine();
            obj.MemberName = memname;
            obj.MemberType = memtype;
            double amount = obj.CalculateMemberFees();
            Console.WriteLine("MemberShip Fees is "+amount);
        }
        else{
            Console.WriteLine("Invalid Member Id");
        }
    }
}






caffeine cove:
using System;
using System.Collections.Generic;
using System.Linq;
public class Coffee{
   
    public string ItemName{get;set;}
    public double Price{get;set;}
}

public class Program{
    public static List<Coffee> CoffeeMenu = new List<Coffee>();
    public static void Main(){
        CoffeeUtility cobj = new CoffeeUtility();
        while(true)
        {
            Console.WriteLine("\n1.Add coffee details");
            Console.WriteLine("2.Update coffee details");
            Console.WriteLine("3.Sort by price");
            Console.WriteLine("4.Exit");
            Console.WriteLine("Enter your Choice");
            int choice = Convert.ToInt32(Console.ReadLine());
           
            if(choice ==1)
            {
                Console.WriteLine("Enter the item name");
                string name = Console.ReadLine();
                Console.WriteLine("Enter price");
                double price = Convert.ToDouble(Console.ReadLine());
                Coffee cd = new Coffee{ItemName = name, Price =price};
                cobj.AddCoffeeDetails(cd);
            }
           
            else if(choice ==2)
            {
                Console.WriteLine("Enter the item name");
                string name = Console.ReadLine();
                Console.WriteLine("Enter price to update");
                double price = Convert.ToDouble(Console.ReadLine());
                List<Coffee> temp = cobj.UpdateCoffeePrice(name,price);
                Console.WriteLine();
                if(temp.Count ==0)
                {
                    Console.WriteLine("No item found");
                }
                else{
                    foreach(Coffee ele in temp)
                    {
                        Console.WriteLine(ele.ItemName+"     "+ele.Price);
                    }
                }
               
            }
            else if(choice ==3)
            {
                List<Coffee> temp = cobj.SortByPrice();
                foreach(Coffee ele in temp)
                {
                    Console.WriteLine(ele.ItemName+"     "+ele.Price);
                }
               
            }
            else if(choice ==4)
            {
                Console.WriteLine("Thank you");
                break;
            }
           
           
        }
    }
}

public class CoffeeUtility{
   
    public void AddCoffeeDetails(Coffee coffeeObj)
    {
        int startlen = Program.CoffeeMenu.Count;
        Program.CoffeeMenu.Add(coffeeObj);
        int finallen = Program.CoffeeMenu.Count;
        if(startlen<finallen)
        {
            Console.WriteLine("Inserted successfully");
        }
        else{
            Console.WriteLine("Insertion failed");
        }
       
    }
   
    public List<Coffee> UpdateCoffeePrice(string itemName, double price)
    {

        foreach(Coffee ele in Program.CoffeeMenu)
        {
            if(ele.ItemName.Equals(itemName))
            {
                ele.Price = price;
                return Program.CoffeeMenu;
               
            }
           
        }
        List<Coffee> newlist = new List<Coffee>();
        return newlist;
       
       
    }
   
    public List<Coffee> SortByPrice()
    {
        var newlist = from str in Program.CoffeeMenu orderby str.Price descending select str;
        return newlist.ToList();
    }
   
}





Unordered Cakes sql:

select Cake_id,Cake_name,Cake_type,Price_per_kg from CAKES where cake_id  not
in(select Cake_id from ORDER_DETAILS) order by cake_name asc;


Recent subscribers:

select  c.CUSTOMER_NAME,s.PLAN_AMOUNT from CUSTOMER c left join SUBSCRIPTION s on C.PHONE_NUMBER = s.PHONE_NUMBER
where month(s.RECHARGE_DATE)BETWEEN 7 and 12 order by c.CUSTOMER_NAME asc;

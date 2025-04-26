//hiii🙏🏼
Код программы:
#include <iostream>
#include <stack>
#include<ctime>
 
using namespace std;
 
struct Stack {
   int info;
   Stack* next;
} *head;
 
Stack* InStuck(Stack* p, int in) {
   Stack* t = new Stack; 
   t->info = in; 
   t->next = p; 
   return t;
}
 
void View(Stack* p) {
   Stack* t = p;
   while (t != NULL) {
       cout << t->info << endl;
       t = t->next;
   }
}
 
int Zadanie_1(Stack* p)
{
   int count = 0;
   Stack* t = p;
   while (t != NULL) {
       count++;
       t = t->next;
   }
   return count;
}
 
void Zadanie_2(Stack* p)
{
   Stack* max = p;
   Stack* min = p;
   Stack* t = p;
   while (t != NULL)
   {
       if (t->info > max->info) max = t;
       else if (t->info < min->info) min = t;
       t = t->next;
   }
   Stack* start = max;
   Stack* end = min;
   if (min->info > max->info) {
       start = min;
       end = max;
   }
 
   t = start->next;
 
   while (t != end)
   {
       Stack* del = t;
       t = t->next;
       delete del;
   }
   start->next = end;
}
 
 
void Delete(Stack** p) 
{
   Stack* t;
   while (*p != NULL) {
   t = *p;
   *p = (*p)->next;
   delete t;
   }
}
void Sort_info1(Stack** p) {
   
   Stack temp;
   temp.info = 0;
   temp.next = *p;
   *p = &temp;
   Stack* t = NULL, * t1, * r;
 
   do {
       for (t1 = *p; t1->next->next != t; t1 = t1->next) {
           if (t1->next->info > t1->next->next->info) {
               r = t1->next->next;
               t1->next->next = r->next;
               r->next = t1->next;
               t1->next = r;
           }
       }
       t = t1->next;
   } while ((*p)->next->next != t);
   //временный
   *p = temp.next;
}
 
 
void Sort_info2(Stack* p) {
   Stack* t = NULL, * t1;
   int r;
   do {
       for (t1 = p; t1->next != t; t1 = t1->next)
           if (t1->info > t1->next->info) {
               
                   r = t1->info;
               t1->info = t1->next->info;
               t1->next->info = r;
           }
       t = t1;
   } while (p->next != t);
}
 
 
int main()
{
   srand(time(NULL));
   setlocale(LC_ALL, "ru");
   int t,n;
   while (true) {
cout << "Выберите действие:\n1)Создание стека;\n2)Добавление элементов;\n3)Просмотр стека;\n4)Выполнение задания;\n5)Cортировкастека 1;\n6)Cортировка стека 2;\n7)Очищение стека;\n\n"; 
   cin >> t;
   switch (t)
   {
   case 1: 
       int k,el;
       if (t == 1 && head != NULL) {
           cout << "Очистите память!" << endl;
           break;
       }
 
       cout << "\nКак вы хотите заполнить стек?\n1)самостоятельно;\n2)Рандомно;\n";
       cin >> k;
       switch (k)
       {
       case 1: cout << "Какое количество элементов вы хотите добавить? ";
           cin >> n;
           for (int i = 1; i <= n; i++)
           {
               cout << "\nВведите " << i << " элемент: \n";
               cin >> el;
               head = InStuck(head, el);
           }
           break;
       case 2:cout << "Какое количество элементов вы хотите добавить? ";
           cin >> n;
           for (int i = 1; i <= n; i++)
           {
               el = rand() % 20 - 10;
               head = InStuck(head, el);
           }
       }
       break;
   case 2: cout << "Какое количество элементов вы хотите добавить? ";
       cin >> n;
       for (int i = 1; i <= n; i++)
       {
           cout << "\nВведите " << i << " элемент: \n";
           cin >> el;
           head = InStuck(head, el);
       }
       break;
   case 3: if (!head) {
       cout << "Cтек пуст!" << endl;
       break;
   }
         cout << " Стек: " << endl;
         View(head);
         break;
   case 4:
       cout<<"\nКоличество элементов стека: "<<Zadanie_1(head)<<endl;
       Zadanie_2(head);
       break;
   case 5: 
       Sort_info1(&head);
       
       break;
   case 6: Sort_info2(head);
       break;
   case 7: Delete(&head);
       break;
   case 0:
       if(head!=NULL)  Delete(&head);
           return 0;
   }
   }
  
   return 0;
}

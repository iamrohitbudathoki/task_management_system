# task_management_system

#include <iostream>
#include<windows.h>
#include<mysql.h>
#include <sstream>
#include<stdio.h>

using namespace std;


void register_user();
void login_user();
void add_task();
void update();
void view();

int main()
{
    int runforever = 1;
    int ans;

    while(runforever == 1){



        cout << endl << endl << "-------------------TASK MANAGEMENT SYSTEM--------------------" << endl<<endl
        << "!                    1. Register New User" << endl
        << "!                    2. Login User" << endl
        << "!                    3. Add New Task" << endl
        << "!                    4. Update Record" << endl
        << "!                    5. View User Details" << endl
        << "!                    6. End" << endl << endl << endl
        <<" ------------------------------------------------------------"<< endl;


        cout << endl << "Your Answer : ";

        cin >> ans;

        switch(ans){
        case 1:
            register_user();
            break;
        case 2:
            login_user();
            break;
        case 3:
            add_task();
            break;
        case 4:
            update();
            break;
        case 5:
            view();
            break;
        case 6:
            runforever = 0;
            break;
        }
    }

    return 0;
}



void register_user(){

    MYSQL* conn;
    conn = mysql_init(0);
    conn = mysql_real_connect(conn, "localhost", "root" , "", "taskmanagementsystem", 0, NULL, 0);

    if(conn){
        int qstate = 0;

        string name, email, password;

        cout << "Enter name : ";
        cin >> name;

        cout << "Enter email : ";
        cin >> email;

        cout << "Enter password : ";
        cin >> password;

        stringstream ss;
        ss << "INSERT INTO user(name, email, password) VALUES('" << name << "','" << email << "'," << password <<")";

        string query = ss.str();
        const char* q = query.c_str();

        qstate = mysql_query(conn, q);
        if(qstate == 0){
            cout << "Record Inserted..." << endl;

        }else{
            cout << "Insert Error" << mysql_error(conn) << endl;

        }
    }else{
        cout << "Connection Error" << endl;


    }

    system("pause");
    system("cls");

}
void login_user(){
 cout<<"Under Construction"<<endl<<endl;
   system("pause");
    system("cls");

}

void add_task(){
cout<<"under construction"<<endl;
 system("pause");
    system("cls");
}

void update(){
    cout<<"under construction!!!"<<endl;

    system("pause");
    system("cls");

}



void view(){

    MYSQL* conn;
    MYSQL_ROW row;
    MYSQL_RES* res;
    conn = mysql_init(0);
    conn = mysql_real_connect(conn, "localhost", "root" , "", "taskmanagementsystem", 0, NULL, 0);
    if(conn){
        int qstate = mysql_query(conn, "SELECT id, name, email FROM user");


        if(!qstate){
            res = mysql_store_result(conn);

            while(row = mysql_fetch_row(res)){
                cout << row[0] <<"\t | \t" << row[1] <<"\t | \t" << row[2] << endl << endl;
             }
        }
    }



    system("pause");
    system("cls");
}

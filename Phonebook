
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
#include<windows.h>
#include<bits/stdc++.h>

using namespace std;

int d=0,item,axisX, axisY;
string cnt;
class Node
{
	public:

	string name;
	string num;


	Node *left;
	Node *right;
	int height;
};
Node *root = NULL;
Node *current=NULL;

void gotoxy(int x, int y){
    COORD coord;
    coord.X=x;
    coord.Y=y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),coord);
}

int height(Node *N)
{
	if (N == NULL)
		return 0;
	return N->height;
}

int max(int a, int b)
{
	return (a > b)? a : b;
}

Node* newNode(string name, string num)
{
	Node* node = new Node();
	node->name = name;
	node->num=num;

	node->left = NULL;
	node->right = NULL;
	node->height = 1; // new node is initially
					// added at leaf
	return(node);
}

Node *rightRotate(Node *y)
{
	Node *x = y->left;
	Node *T2 = x->right;
	x->right = y;
	y->left = T2;

	y->height = max(height(y->left),
					height(y->right)) + 1;
	x->height = max(height(x->left),
					height(x->right)) + 1;

	return x;
}

Node *leftRotate(Node *x)
{
	Node *y = x->right;
	Node *T2 = y->left;

	y->left = x;
	x->right = T2;

	x->height = max(height(x->left),
					height(x->right)) + 1;
	y->height = max(height(y->left),
					height(y->right)) + 1;

	return y;
}

int getBalance(Node *N)
{
	if (N == NULL)
		return 0;
	return height(N->left) - height(N->right);
}

Node* insert(Node* node, string name,string num)
{
	if (node == NULL)
		return(newNode(name,num));

	if (name < node->name)
		node->left = insert(node->left, name,num);
	else if (name > node->name)
		node->right = insert(node->right,name,num);
	else 
		return node;

	node->height = 1 + max(height(node->left),
						height(node->right));

	int balance = getBalance(node);

	if (balance > 1 && name < node->left->name)
		return rightRotate(node);


	if (balance < -1 && name > node->right->name)
		return leftRotate(node);


	if (balance > 1 && name > node->left->name)
	{
		node->left = leftRotate(node->left);
		return rightRotate(node);
	}

	if (balance < -1 && name < node->right->name)
	{
		node->right = rightRotate(node->right);
		return leftRotate(node);
	}

	return node;
}

Node * minValueNode(Node* node)
{
    Node* current = node;
    while (current->left != NULL)
        current = current->left;

    return current;
}

Node* deleteNode(Node* root, string name)
{

    if (root == NULL)
        return root;
    if ( name < root->name )
        root->left = deleteNode(root->left, name);

    else if( name > root->name )
        root->right = deleteNode(root->right, name);

    else
    {
       
        if( (root->left == NULL) ||
            (root->right == NULL) )
        {
            Node *temp = root->left ?
                         root->left :
                         root->right;

     
            if (temp == NULL)
            {
                temp = root;
                root = NULL;
            }
            else // One child case
            *root = *temp; // Copy the contents of
                           // the non-empty child
            free(temp);
        }
        else
        {
            
            Node* temp = minValueNode(root->right);

          
            root->name = temp->name;
            root->num = temp->num;

            
            root->right = deleteNode(root->right,
                                     temp->name);
        }
    }
    if (root == NULL)
    return root;
    root->height = 1 + max(height(root->left),
                           height(root->right));

    int balance = getBalance(root);

    if (balance > 1 &&
        getBalance(root->left) >= 0)
        return rightRotate(root);
    if (balance > 1 &&
        getBalance(root->left) < 0)
    {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    if (balance < -1 &&
        getBalance(root->right) <= 0)
        return leftRotate(root);
    if (balance < -1 &&
        getBalance(root->right) > 0)
    {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}
void preOrder(Node *root)
{
	if(root != NULL)
	{

		preOrder(root->left);
        gotoxy(axisX,axisY);
        cout << root->name;
        gotoxy(axisX+30,axisY++);
        cout << root->num;
		preOrder(root->right);

	}
}
void deleteContact();

void search(Node *root,string s){



    if(root==NULL)
        return;
    string alt=s;
    alt[0]=toupper(s[0]);
    string stemp= root->name;
        search(root->left,s);
        size_t found = root->name.find(s);
        size_t found2 = root->name.find(alt);
         if(found != string::npos && found==0 || found2 != string::npos && found2==0)
        {
            item++;
           
            gotoxy(axisX,axisY);
            cout << root->name;
            gotoxy(axisX+30,axisY++);
            cout << root->num;
            cnt=root->name;
            current=root;
        }
        search(root->right,s);
}
void mainMenu();
void altUI();
void viewContacts(){
    system("cls");
    gotoxy(40,1);
    cout << "All Contacts\n";
    gotoxy(25,3);
    cout << "Contact Name";
    gotoxy(55,3);
    cout << "Contact No\n";
    gotoxy(25,4);
    cout<<"----------------------------------------";
    axisX=25;
    axisY=5;
    preOrder(root);
    return;
}
void editContact(){
    system("cls");
        viewContacts();
        printf("\n\n\tEnter name: ");
        cin >> cnt;
        system("cls");
        gotoxy(25,3);
        cout << "Contact Name";
        gotoxy(55,3);
        cout << "Contact No\n";
        gotoxy(25,4);
        cout<<"----------------------------------------";
        axisX=25;
        axisY=5;
        search(root,cnt);
        if(item==0){
            cout << "\n\t\t\t\tNo contact found!\n";
            getch();
            editContact();
        }
        else if(item==1){
            char edit[100];
            string unchanged;
            cout << "\n\n\t1.\tEdit\n\t2.\tCancel\n\tConfirm edit: ";
            scanf("%d",&d);
            if(d==1){
                int c;
                cout << "\n\n\t\t1. Edit Name.    2. Edit Contact No.    3. Cancel.\n\t\tSelect: ";
                scanf("%d",&c);
                if(c==1){
                    cout<<"\nEnter new Name: ";
                    scanf("\n%[^\n]",edit);
                    edit[0]=toupper(edit[0]);
                    //cout<<edit;
                    unchanged=current->num;
                    deleteNode(root,current->name);
                    insert(root,edit,unchanged);
                }else if(c==2){
                    cout<<"\nEnter new Contact No: ";
                    cin>>edit;

                    unchanged=current->name;
                    deleteNode(root,current->name);
                    insert(root,unchanged,edit);
                    //current->num=edit;
                }
                else{
                    item=0;
                    return;
                }
                cout << "\n\t\t\t\tContact edited!\n";
                cout<<"\nPress any key to continue...";
                getch();
                item=0;
                return;
            }
            else{
                item=0;
                return;
            }
        }
        else{
            cout << "\n\n\t\tToo many choices. Be more specific...\n";
            getch();
            item=0;
            editContact();
        }
}
void deleteContact(){
        system("cls");
        viewContacts();
        printf("\n\n\tEnter name: ");
        cin >> cnt;
        system("cls");
        gotoxy(25,3);
        cout << "Contact Name";
        gotoxy(55,3);
        cout << "Contact No\n";
        gotoxy(25,4);
        cout<<"----------------------------------------";
        axisX=25;
        axisY=5;
        search(root,cnt);
        if(item==0){
            cout << "\n\t\t\t\tNo contact found!\n";
            getch();
            deleteContact();
        }
        else if(item==1){
            cout << "\n\n\t1.\tDelete\n\t2.\tCancel\n\tConfirm delete:\n";
            scanf("%d",&d);
            if(d==1){
                deleteNode(root,cnt);
                cout << "\n\t\t\t\tContact deleted!\n";
                cout<<"\nPress any key to continue...";
                getch();
                item=0;
                return;
            }
            else{
                item=0;
                return;
            }

        }
        else{
            cout << "\n\n\t\tToo many choices. Be more specific...\n";
            getch();
            item=0;
            deleteContact();
        }
}

void searchContact(){
    system("cls");
    cout << "\tEnter contact: ";
    cin >> cnt;
    gotoxy(25,3);
    cout << "Contact Name";
    gotoxy(55,3);
    cout << "Contact No\n";
    gotoxy(25,4);
    cout<<"----------------------------------------";
    axisX=25;
    axisY=5;
    search(root,cnt);
    if(item==1){
        cout << "\n\t\t\t\t\tEnd of results...";
        printf("\n\n\t1. Edit\n\t2. Delete\n\t3. Cancel\n\n\tSelect: ");
        scanf("%d",&d);
        if(d==1){
            item=0;
            //editContact();
        }
        else if(d==2){
            item=0;

            deleteNode(root,cnt);
            cout << "\n\t\t\t\tContact deleted!\n";
            cout<<"\nPress any key to continue...";
            getch();
        }else{
            item=0;

            return;
        }
    }
    else{
        cout << "\n\t\t\t\t\tEnd of results...";
        item=0;
        cout<<"\nPress any key to continue...";
            getch();
        return;
    }
}
void insertContact(){
    char fname[100];
    char lname[100];
    string contact;
    cout << "\n\tEnter first name: ";
    cin >> fname;
    fname[0]=toupper(fname[0]);
    cout << "\n\tEnter last name: ";
    cin >> lname;
    strcat(fname," ");
    strcat(fname,lname);
    cout << "\tEnter contact no: ";
    cin >> contact;
    root = insert(root,fname,contact);
    cout << "\nInsert successful!";
    getch();
}
void mainMenu(){

    system("cls");
    axisX=25;
    axisY=3;
    printf("\n\n\n\n\t\t\t\t1.\tView Contacts.\n");
    printf("\t\t\t\t2.\tNew Contact.\n");
    printf("\t\t\t\t3.\tEdit Contacts.\n");
    printf("\t\t\t\t4.\tDelete Contacts.\n");
    printf("\t\t\t\t5.\tSearch Contacts.\n");
    printf("\t\t\t\t6.\tExit.\n");
    printf("Select: ");
    scanf("%d",&d);
    if(d==1){
        viewContacts();
        printf("\n\nPress any key to return to main menu...\n");
        getch();
        mainMenu();
    }else if(d==2){
        insertContact();
        mainMenu();
    }else if(d==3){
        editContact();
        mainMenu();
    }else if(d==4){
        deleteContact();
        mainMenu();
    }else if(d==5){
        searchContact();
        mainMenu();
    }else exit(0);

}
void altUI(){
    system("cls");
    viewContacts();
    cout << "\n\n\t\t1. Insert new    2. Delete    3. Search    4. Edit    5. Exit";
        printf("\n\t\tSelect: ");
    scanf("%d",&d);
    if(d==1){
        insertContact();
        altUI();
    }else if(d==2){
        deleteContact();
        altUI();
    }else if(d==3){
        searchContact();
        altUI();
    }else if(d==4){
        editContact();
        altUI();
    }else{
        exit(0);
    }
}
int main()
{
    root = insert(root,"Wasif Fuad","0178952");
    root = insert(root,"Fuad Ahmed","01789980207");
    root = insert(root, "Kamrul Hasan","4891561");
    root = insert(root, "Abbas Ali","447855");
    root = insert(root, "Amir Hossain","44582125");
    root = insert(root, "Nahid Reza","23145421");
    root = insert(root,"Masud Rana","523132");
    root = insert(root, "Jack Nicholson","426355");
    root = insert(root, "Pranto Mirza","4548514");
    root = insert(root, "Arnob Ahmed","4548514");

    gotoxy(45,10);
    printf("1. UI-1\n");
    gotoxy(45,11);
    printf("2. UI-2\n");
    gotoxy(45,13);
    printf("Select: ");
    scanf("%d",&d);
    if(d==1)mainMenu();
    else altUI();
}

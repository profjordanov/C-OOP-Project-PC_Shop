// PC_Shop.cpp : Defines the entry point for the console application.
//
#include "stdafx.h"
#include <iostream>
#include <Windows.h> // For coord
#include <string>
#include <fstream>
#include <vector>

using namespace std;

//Positioning the cursor
void gotoxy(short x, short y) {
	COORD coord;
	coord.X = x;
	coord.Y = y;
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}
//Info for Course work
void info() {
	system("cls");
	system("color 02");
	gotoxy(1, 2);
	cout << ("               OBJECT-ORIENTED PROGRAMING COURSEWORK               \n");
	cout << ("=======================================================================\n");
	cout << ("                     WELCOME TO COMPUTER SHOP                      \n");
	cout << ("=======================================================================\n");
	cout << ("=======================================================================\n");
	gotoxy(1, 9);
	cout << ("                   University of economics - Varna                 \n");
	cout << ("=======================================================================\n");
	gotoxy(1, 11);
	cout << ("            SUBJECT TEACHER: Prof. Dr. Pavel Petrov              \n");
	cout << ("                   ASSISTANT: Valentin Atanasov                    \n");
	cout << ("=======================================================================\n");
	cout << ("=======================================================================\n");
	gotoxy(0, 16);
	cout << (" BY:     Iskra Petrova, Meral Mustafova Nadia Geneva , Yordan Yordanov\n");
	cout << (" COURSE: 2                                                        \n");
	cout << (" GROUP:  39                                                       \n");
	cout << (" FN :    103 410 , 103 207 , 102 898 , 102 878                    \n");
	gotoxy(0, 21);
	cout << ("=======================================================================\n");
	cout << ("                         YEAR: 2015-2016                             \n");
	cout << ("=======================================================================\n");
	gotoxy(1, 24);
	cout << (" PRESS ENTER TO CONTINUE!!!!!!");
	cin.get();
	system("cls");
}
class pcitem {
public:
	virtual void printInfo() = 0;
	virtual string printToFile() = 0;
protected:
	string brand;
	double price;
};
class procesor :public pcitem {
public:
	procesor(string b, string model, string frequency, double pr) {
		brand = b;
		price = pr;
		this->frequency = frequency;
		this->model = model;
	}
	virtual void printInfo() {
		cout << "CPU " << "Brand: " << brand << "\t\t" << " Model: " << model << "\t\t\t" << " Frequency: " << frequency << "\t" << " Price: " << price << endl;
	}
	virtual string printToFile() {
		fstream itemsFile("F:\\itemsList.txt", ios::app);
		return "CPU\t" + brand + "\t" + model + "\t" + frequency + "\t" + to_string(price) + "\n";
	}
private:
	string frequency;
	string model;
};
class ram :public pcitem {
public:
	ram(string b, string model, string frequency, string size, double pr) {
		brand = b;
		price = pr;
		this->frequency = frequency;
		this->size = size;
		this->model = model;
	}
	virtual void printInfo() {
		cout << "RAM " << "Brand: " << brand << "\t\t" << " Model: " << model << "\t\t" << " Size: " << size << "\t" << " Frequency: " << frequency << "\t" << " Price: " << price << endl;
	}
	virtual string printToFile() {
		fstream itemsFile("F:\\itemsList.txt", ios::app);
		return "RAM\t" + brand + "\t" + model + "\t" + size + "\t" + frequency + "\t" + to_string(price) + "\n";
	}
private:
	string frequency;
	string size;
	string model;
};
class gpu :public pcitem {
public:
	gpu(string b, string model, string size, double pr) {
		brand = b;
		price = pr;
		this->size = size;
		this->model = model;
	}
	virtual void printInfo() {
		cout << "GPU " << "Brand: " << brand << "\t\t" << " Model:" << model << "\t\t" << " Size: " << size << "\t\t\t\t" << " Price: " << price << endl;
	}
	virtual string printToFile() {
		fstream itemsFile("F:\\itemsList.txt", ios::app);
		return "GPU\t" + brand + "\t" + model + "\t" + size + "\t" + to_string(price) + "\n";
	}
private:
	string size;
	string model;
};
class hardDrive : public pcitem {
public:
	hardDrive(string b, string size, double pr) {
		brand = b;
		price = pr;
		this->size = size;
	}
	virtual void printInfo() {
		cout << "HDD " << "Brand: " << brand << "\t\t\t\t\t" << " Size: " << size << "\t\t\t\t" << " Price: " << price << endl;

	}
	virtual string printToFile() {
		fstream itemsFile("F:\\itemsList.txt", ios::app);
		return "HDD\t" + brand + "\t" + size + "\t" + to_string(price) + "\n";
	}
private:
	string size;
};
class itemss {
public:
	itemss(string fileName);
	void add(pcitem *p);
	void list();
	int writeToFile();
	string choice(int n);
protected:
	vector< pcitem * > v;
	string itemsFile;
};
//Prochita faila i go pylni vyv vektora
itemss::itemss(string itemsFile) {
	this->itemsFile = itemsFile;
	itemsFile = "F:\\itemsList.txt";
	fstream inputStream(itemsFile, ios::in);

	if (!inputStream.is_open()) {
		cerr << "nope";
		return;
	}

	string type, brand, model, frequency, price, size;
	while (!inputStream.eof()) {
		getline(inputStream, type, '\t');
		if (type == "CPU") {
			getline(inputStream, brand, '\t');
			getline(inputStream, model, '\t');
			getline(inputStream, frequency, '\t');
			getline(inputStream, price);
			this->v.push_back(new procesor(brand, model, frequency, stod(price)));
		}
		if (type == "RAM") {
			getline(inputStream, brand, '\t');
			getline(inputStream, model, '\t');
			getline(inputStream, frequency, '\t');
			getline(inputStream, size, '\t');
			getline(inputStream, price);
			this->v.push_back(new ram(brand, model, frequency, size, stod(price)));
		}
		if (type == "GPU") {
			getline(inputStream, brand, '\t');
			getline(inputStream, model, '\t');
			getline(inputStream, size, '\t');
			getline(inputStream, price);
			this->v.push_back(new gpu(brand, model, size, stod(price)));
		}
		if (type == "HDD") {
			getline(inputStream, brand, '\t');
			getline(inputStream, size, '\t');
			getline(inputStream, price);
			this->v.push_back(new hardDrive(brand, size, stod(price)));
		}
	}
};
//dobavq nov item
void itemss::add(pcitem *p) {
	v.push_back(p);
}
// zapisva vyv faila item
int itemss::writeToFile() {
	fstream outputStreamItems("F:\\itemsList.txt", ios::out);
	if (!outputStreamItems.is_open()) {
		cerr << "Cannot open file!";
		return -1;
	}

	for (int i = 0; i < v.size(); i++) {
		outputStreamItems << v[i]->printToFile();
	}
	return 0;
}
void itemss::list() {
	for (int i = 0; i < v.size(); i++) {
		cout << i + 1 << ". ";
		v[i]->printInfo();
	}
	cout << "=====\nTOTAL: " << v.size() << endl;
}
string itemss::choice(int n) {
	return v[n]->printToFile();
}
class orders {
public:
	virtual void printInfo() = 0;
	virtual string printToFile() = 0;
protected:
	double total;
	string components;
	string name;
};
class orderList :public orders {
public:
	orderList(string n, string phone, string comp, double to) {
		total = to;
		name = n;
		this->phone = phone;
		this->components = comp;
	}
	virtual void printInfo() {
		cout << "Name  " << name << "\tPhone: " << phone << "\tItems: " << components << "\tTotal: " << total << endl;
	}
	virtual string printToFile() {
		fstream orders("F:\\orders.txt", ios::app);
		return name + "\t" + phone + "\t" + components + "\t" + to_string(total) + "\n";
	}
protected:
	string phone;
};
class order {
public:
	order(string fileName);
	void add(orders *po);
	void list();
	int writeToFile();
	string choice(int n);
private:
	vector< orders * > o;
	string file;
};
order::order(string file) {
	this->file = file;
	file = "F:\\orders.txt";
	fstream inputStreamO(file, ios::in);

	if (!inputStreamO.is_open()) {
		cerr << "nope";
		return;
	}
	string name, phone, components, total;
	while (!inputStreamO.eof()) {
		if (name == "\n") break;
		getline(inputStreamO, name, '\t');
		getline(inputStreamO, phone, '\t');
		getline(inputStreamO, components, '\t');
		getline(inputStreamO, total);
		this->o.push_back(new orderList(name, phone, components, stod(total)));
	}
};
void order::add(orders *po) {
	o.push_back(po);
}
void order::list() {
	for (int i = 0; i < o.size(); i++) {
		cout << i + 1 << ". ";
		o[i]->printInfo();
	}
	cout << "=====\nTOTAL: " << o.size() << endl;
}
int order::writeToFile() {
	fstream outputStreamOrder("F:\\orders.txt", ios::out);
	if (!outputStreamOrder.is_open()) {
		cerr << "Cannot open file!";
		return -1;
	}

	for (int i = 0; i < o.size(); i++) {
		outputStreamOrder << o[i]->printToFile();
	}
	return 0;
}
string order::choice(int n) {
	return o[n]->printToFile();
}
void showMenu() {
	system("cls");
	gotoxy(0, 2);
	cout << ("========================================\n");
	cout << "    Welcome to \"U.E.V\" Computer Shop\n";
	cout << ("========================================\n");
	cout << "           1. New Order\n";
	cout << "           2. Add PC item\n";
	cout << "           3. Modify order\n";
	cout << "           4. List orders \n";
	cout << "           5. Info for Course Work \n";
	cout << "           0. Exit \n";
	cout << ("========================================\n");
	cout << "  Enter your Selection: ";
}
//menu items
void additems() {
	system("cls");
	gotoxy(0, 2);
	cout << ("========================================\n");
	cout << "                Add Item\n";
	cout << ("========================================\n");
	cout << "           1. CPU\n";
	cout << "           2. RAM\n";
	cout << "           3. GPU\n";
	cout << "           4. HardDrive\n";
	cout << "           0. Back to menu\n";
	cout << ("========================================\n");
	cout << "  Enter your Selection: ";
}

int main()
{
	info();
	itemss item("F:\\itemsList.txt");
	order ord("F:\\orders.txt");
	string brand, size, frequency, model;
	double price;
	//Menu
	string chm = "9";
	while (chm != "0")
	{
		showMenu();
		getline(cin, chm);
		if (chm == "0") {
			int success = item.writeToFile();
			int successOrd = ord.writeToFile();
			if (success == -1 && successOrd == -1) {
				chm = 999;
				continue;
			}
			return 0;
		}
		else if (chm == "1") {
			string name, phone, comp, si, c = "n";
			double total = 0.0;
			int porednoChislo;
			vector<string> izbrani;
			orderList *norderList = new orderList(name, phone, comp, total);
			system("cls");
			gotoxy(0, 2);
			cout << ("========================================\n");
			cout << "                New Order\n";
			cout << ("========================================\n");
			cout << " Name: "; getline(cin, name);
			cout << " Phone: "; getline(cin, phone);
			cout << "Items: " << endl;
			item.list();
			cout << "vyvedete nomera na izbraviq item i natisnete Enter( izbiranete prikluchva s vyvejdaneto na 0)" << endl;
			while (true)
			{
				cout << "Item: ";
				cin >> porednoChislo;
				if (porednoChislo == 0)	break;
				else {
					string s = item.choice(porednoChislo - 1);
					for (int i = 0; i < s.size(); i++) {
						if (s[i] == '\t') s[i] = ' ';
					}
					int begin = s.find_first_not_of("\n");
					int end = s.find_last_not_of("\n");
					s = s.substr(begin, end - begin);
					izbrani.push_back(s);
				}
			}
			cout << ("========================================\n");
			for (int i = 0; i < izbrani.size(); i++) {
				int price;
				string p;
				price = izbrani[i].find_last_of(" ");
				p = izbrani[i].substr(price);
				total += stod(p);
			}
			cout << "TOTAL Price is: " << total << endl;
			cout << "Do you want to make a order?(y/n): ";
			cin >> c;
			if (c == "n") showMenu();
			else {
				string items;
				for (int i = 0; i < izbrani.size(); i++) {
					si = izbrani[i];
					int nif = si.find_first_not_of("\n");
					int nie = si.find_last_not_of("\n");
					if (i + 1 < izbrani.size()) {
						items += si.substr(nif, nie - nif) + "|";
					}
					else {
						items += si.substr(nif, nie - nif);
					}
				}
				ord.add(new orderList(name, phone, items, total));
			}
		}
		else if (chm == "2") {
			string chi = "9";
			while (chi != "0") {
				additems();
				getline(cin, chi);
				if (chi == "0") {
					showMenu();
				}
				else if (chi == "1") {
					string brand, model, frequency;
					double price = 0.0;
					procesor *nprocesor = new procesor(brand, model, frequency, price);
					system("cls");
					gotoxy(0, 2);
					cout << ("========================================\n");
					cout << "                Add CPU\n";
					cout << ("========================================\n");
					cout << " Brand: "; getline(cin, brand);
					cout << " Model: "; getline(cin, model);
					cout << " Frequency: "; getline(cin, frequency);
					cout << " Price: "; cin >> price;
					cout << ("========================================\n");
					item.add(new procesor(brand, model, frequency, price));
				}
				else if (chi == "2") {
					string brand, model, frequency, size;
					double price = 0.0;
					ram *nram = new ram(brand, model, frequency, size, price);
					system("cls");
					gotoxy(0, 2);
					cout << ("========================================\n");
					cout << "                Add RAM\n";
					cout << ("========================================\n");
					cout << " Brand: "; getline(cin, brand);
					cout << " Model: "; getline(cin, model);
					cout << " Frequency: "; getline(cin, frequency);
					cout << " Size: "; getline(cin, size);
					cout << " Price: "; cin >> price;
					cout << ("========================================\n");
					item.add(new ram(brand, model, frequency, size, price));
				}
				else if (chi == "3") {
					string brand, model, frequency, size;
					double price = 0.0;
					gpu *ngpu = new gpu(brand, model, size, price);
					system("cls");
					gotoxy(0, 2);
					cout << ("========================================\n");
					cout << "                Add GPU\n";
					cout << ("========================================\n");
					cout << " Brand: "; getline(cin, brand);
					cout << " Model: "; getline(cin, model);
					cout << " Size: "; getline(cin, size);
					cout << " Price: "; cin >> price;
					cout << ("========================================\n");
					item.add(new gpu(brand, model, size, price));
				}
				else if (chi == "4") {
					string brand, model, frequency, size;
					double price = 0.0;
					hardDrive *nhardDrive = new hardDrive(brand, size, price);
					system("cls");
					gotoxy(0, 2);
					cout << ("========================================\n");
					cout << "                Add Hard Driven\n";
					cout << ("========================================\n");
					cout << " Brand: "; getline(cin, brand);
					cout << " Size: "; getline(cin, size);
					cout << " Price: "; cin >> price;
					cout << ("========================================\n");
					item.add(new hardDrive(brand, size, price));
				}
			}
		}
		else if (chm == "3")
		{
			ord.list();
			system("pause");
		}
		else if (chm == "4") {
			int number;
			system("cls");
			gotoxy(0, 2);
			cout << ("========================================\n");
			cout << "                Modify order\n";
			cout << ("========================================\n");
			ord.list();
			cout << ("========================================\n");
			cout << "vyvedete nomera na izbraviq order i natisnete Enter(0.Back to menu)" << endl;
			cin >> number;
			if (number == 0)	break;
			else
			{
				cout << "Ne znam kak stava";
				system("pause");
			}
		}
		else if (chm == "5"){
			info();
		}
	}
	return 0;
}

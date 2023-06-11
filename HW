#include <stdio.h>
#include <stdlib.h>
#include <iostream>
#include <fstream>
#include <string.h>
#include <vector>
#include <algorithm>
#include <cstdlib>

using namespace std;

typedef struct {
	string instruction ;
	int site ;
	int folder ;
} tableitem;

class Mission {
	public:
		vector<tableitem> table1 ;
		vector<tableitem> table2 ;
		vector<tableitem> table3 ;
		vector<tableitem> table4 ;
		vector<tableitem> alltable ;
		tableitem table5[100] ;   // label
		tableitem table6[100] ;   // num
		tableitem table7[100] ;   //  something in' '
		vector<string> token ;  //讀進來的東西 
		vector<tableitem> linetemp ;  // 暫放每一行 
		void readtable() ;
		void readtxt () ;
		void cutoken() ;
		void t4push(char ch) ;
		void hastable7( string str ) ;
		bool isnum(string str) ;
		bool isletter(string str) ;
		int hastable6(string str) ;
		int hastable5(string str) ;
		void inwhich(string str) ;
		bool intable4( char ch ) ;
		string caps(string voc) ;
		bool findt5 (string str, int& table) ;
		void clear() ;
};

void Mission::readtable() {
	fstream tabledata ;
	string name1 = "Table1.table" ;
	string name2 = "Table2.table" ;
	string name3 = "Table3.table" ;
	string name4 = "Table4.table" ;
	tableitem temp ;
	string ftemp ;
	
	tabledata.open(name1.c_str(),fstream::in ) ;	
	for(int i = 1 ; !tabledata.eof() ; i++) { // read table1 
	  tabledata >> ftemp ;
	  ftemp = caps(ftemp);
	  temp.instruction = ftemp ;
	  temp.site = i ;
	  temp.folder = 1 ;
	  table1.push_back(temp) ;
	  alltable.push_back(temp) ;
    }
    tabledata.close() ;
    ftemp.clear() ;
    
    
    tabledata.open(name2.c_str(),fstream::in ) ;	
	for(int i = 1 ; !tabledata.eof() ; i++) {	// read table2
	  tabledata >> ftemp ;
	  temp.instruction = ftemp ;
	  temp.site = i ;
	  temp.folder = 2 ;
	  table2.push_back(temp) ;
	  alltable.push_back(temp) ;
    }
    tabledata.close() ;
    ftemp.clear() ;
    
    
    tabledata.open(name3.c_str(),fstream::in ) ;	
	for(int i = 1 ; !tabledata.eof() ; i++) {	// read table3
	  tabledata >> ftemp ;
	  temp.instruction = ftemp ;
	  temp.site = i ;
	  temp.folder = 3 ;
	  table3.push_back(temp) ;
	  alltable.push_back(temp) ;
    }
    tabledata.close() ;
    ftemp.clear() ;
    
    
   	tabledata.open(name4.c_str(),fstream::in ) ;	
	for(int i = 1 ; !tabledata.eof() ; i++) {	// read table4
	  tabledata >> ftemp ;
	  temp.instruction = ftemp ;
	  temp.site = i ;
	  temp.folder = 4 ;
	  table4.push_back(temp) ;
	  alltable.push_back(temp) ;
    }
    tabledata.close() ;
    ftemp.clear() ;


    //for ( int i = 0 ; i < alltable.size() ; i++ )
    	//cout << alltable[i].folder << " " << alltable[i].site << " " << alltable[i].instruction << endl ;
     
}

void Mission::readtxt (){ 	// read the input txt 
	fstream txt ; 
	string lname = "" ;
	string name = "" ;
	string aline = "" ;

		
	do {
		cout << "Input a file name: " ;
		cin >> name ;
		lname = "SIC_" + name + ".txt" ;
		txt.open(lname.c_str(), fstream::in) ;
		if(txt.is_open()) {
			while ( getline(txt,aline) ) token.push_back(aline) ;
			break;
		}
		else {
			cout << "File isn't exist" ;
			break ;
		}
	    
	} while(true) ;
	//for (int i = 0; i < token.size();  i++)
		//cout << token[i] << endl ;
}

void Mission::cutoken (){   // get token
	string outname =  "SIC_Output.txt" ;
	string atoken = "" ;
	ofstream outfile (outname.c_str()) ;
	tableitem temp ;
	int numtable = 0 ;
	
	for(int line = 0; line < token.size(); line++ ) {
		for(int letter = 0; letter < token[line].size(); letter++ ) {
			
			if ( (token[line][letter] != ' ' && token[line][letter] != '\t') ) {    
				if( token[line][letter+1] == 39  && ( token[line][letter] == 'C' || token[line][letter] == 'c'  
						|| token[line][letter] == 'X' || token[line][letter] == 'x') ) {    
					
					letter++ ;	// -> '
					t4push(token[line][letter]) ;   // 將'加入陣列 
					if ( token[line][letter-1] == 'C' || token[line][letter-1] == 'c' ) {
						letter++ ;
						while( token[line][letter] != 39){     //讀' '中間的字 
							atoken = atoken + token[line][letter] ;
							letter++ ;
						}
						hastable7(atoken) ;
						atoken = "" ;
						//letter++ ;	// -> '
						t4push(token[line][letter]) ;   // 將'加入陣列 
					}						
					else if ( token[line][letter-1] == 'x' || token[line][letter-1] == 'X' ) {
						letter++ ;
						while( token[line][letter] != 39){     //讀' '中間的字 
							atoken = atoken + token[line][letter] ;
							letter++ ;
						}
						
						numtable = hastable6(atoken) ;
						
						temp.instruction = atoken ;
						temp.folder = 6 ;
						temp.site = numtable ;
						linetemp.push_back(temp) ;
									

						t4push(token[line][letter]) ;   // 將'加入陣列 
					} 	
				} // if for c and x
				else if( intable4(token[line][letter]) == true ) {    //  如果在第4個table
					if( atoken != " " && atoken != "" )
						inwhich(atoken) ;   // 把前面不是table4的先處理掉
					atoken = "" ;       //清空atoken
					
					t4push(token[line][letter]) ;
					atoken = "" ;
					if(token[line][letter] == '.'){    // 如果是table4的" . " 
         				while(  letter < token[line].size() ) letter++ ; 	 
					}//if
							 		
				}//if		
						

				else if ( token[line][letter] != ' ' && token[line][letter] != '\t' ) {
					while ( letter < token[line].size() && (token[line][letter] != ' ' && token[line][letter] != '\t' ) && !intable4(token[line][letter])) {
						atoken = atoken + token[line][letter] ;
						letter ++ ;
					}
					letter -- ;
//					cout << atoken << "-" << endl;
					inwhich(atoken) ;
					atoken = "" ;
				}
								

					
			} // if for not ' ' , tab
			
		}//if  letter
		
		outfile << token[line] << "\n" ;
		for( int a = 0 ; a < linetemp.size() ; a++ ){
			outfile << "(" << linetemp[a].folder << "," << linetemp[a].site << ") " << " " ;
		}
		outfile << "\n" ;
		atoken = "" ;
		linetemp.clear() ;
	}//for  line

		
	outfile.close();
}

void Mission::hastable7( string str ) {  
	int total = 0 ;
	bool arrival = false ;
	tableitem temp ;
	for ( int i = 0 ; i < str.size() ; i ++ ) {
		total = total + (int)str[i] ;
		total %= 100 ;
	}
	if ( table7[total].instruction == str ) {
		temp.instruction = str ;
		temp.folder = 7 ;
		temp.site = total;
		linetemp.push_back(temp) ;
	}
	else{
		while ( arrival == false ) {
			if ( table7[total].instruction == "" ) {
				table7[total].instruction = str ;
				table7[total].site = total ;
				table7[total].folder = 7 ;
				arrival = true ;
			}
			total += 1 ;
			total %= 100 ;
		}
		total -= 1 ;
		temp.instruction = str ;
		temp.folder = 7 ;
		temp.site = total;
		linetemp.push_back(temp) ;
	}
	
}

bool Mission::isnum(string str) {    // is num
    for( int i = 0 ; i < str.size() ; i++ ) {	
		if( str[i]>=48 && str[i]<=57 ) {
    		if( i == str.size() - 1 ) 
    		  return true ;
    		
	  	}
	  	else 
			return false ;
	}
}

bool Mission::isletter(string str) {     //   is word
	string tcaps ;
	tcaps = caps( str ) ;
    for( int i = 0 ; i < tcaps.size() ; i++ ) {	
		if( ( tcaps[i]>='A' && tcaps[i]<='Z' ) ) {
    		if( i == tcaps.size() - 1 )
    		  return true ;
    		
	  	}
	  	else 
			return false ;
	}
}

int Mission::hastable6(string str) {
	int site = 0 ;
	for(int i=0; i<100 && str[i] !=NULL; i++) {
    	site = site + (int)str[i] ; 
    }
	site %= 100 ;
	if ( table6[site].instruction == str ) 
		return site;
	else
		while(table6[site].instruction != "" && table6[site].instruction != str) site++ ;
		table6[site].instruction = str ;
		return site ;
}

int Mission::hastable5(string str) {
	int site = 0 ;

	for(int i=0; i<str.size() ; i++) {
	    site = site + (int)str[i] ; 
	}
	site %= 100 ;
		
	if ( table5[site].instruction == str ) 
		return site ;
	else{
		while(table5[site].instruction != "" && table5[site].instruction != str) 
			site++ ;
		table5[site].instruction = str ;
		return site ;
	}

}

void Mission::inwhich(string str){   // 看是哪個table並放進去 
	tableitem temp ;
	string tcaps ;
	int sites = 0;
	tcaps = caps( str ) ;
	bool is14table = false ;
	int table = 0 ;
	for(int i = 0 ; i < alltable.size() ; i++) {             // 檢查是1-4table嗎 
		if(tcaps.compare(alltable[i].instruction) == 0) {    //放進去 
			temp.instruction = alltable[i].instruction ;
			temp.folder = alltable[i].folder ;
			temp.site = alltable[i].site ;
			linetemp.push_back(temp) ;
			is14table = true ;
		}//if
	}//for
	          // 是table6嗎 
	if (is14table == false){             //  是table5嗎 
		if(isnum(tcaps) ) {   //放進去 
			sites = hastable6(tcaps) ;
			temp.instruction = tcaps ;
			temp.folder = 6 ;
			temp.site = sites ;
			linetemp.push_back(temp) ;
		}
	}//if
	
	if (is14table == false){             //  是table5嗎 
		if(isletter(tcaps) ) {   //放進去 
			sites = hastable5(tcaps) ;
			temp.instruction = tcaps ;
			temp.folder = 5 ;
			temp.site = sites ;
			linetemp.push_back(temp) ;
		}
	}//if
} 

bool Mission::intable4( char ch ) {    //  如果是table4 
	tableitem temp ;
	string tch = "" ;
	tch = ch ;
	for(int i = 0 ; i < table4.size() ; i++) {
		if(tch.compare(table4[i].instruction) == 0)
			return true ;
		
		
	}
	return false ;
}

string Mission::caps(string voc) {    // 大小寫的切換
	for ( int i = 0 ; i < voc.size() ; i ++ ) {
		if ( 'a' <= voc[i] && voc[i] <= 'z' ) {
			voc[i] = voc[i] - 32 ;
		} 
	} 
	return voc ;
}

void Mission:: t4push(char ch){
	string str = "" ;
	str = ch ;
	tableitem temp ;
	for(int i = 0 ; i < table4.size() ; i++) {             
		if(str.compare(table4[i].instruction) == 0) {    
			temp.instruction = table4[i].instruction ;
			temp.folder = table4[i].folder ;
			temp.site = table4[i].site ;
			linetemp.push_back(temp) ;
		}//if
	}
}

void Mission::clear(){
	token.clear() ;
	linetemp.clear() ;
	table1.clear() ;
	table2.clear() ;
	table3.clear() ;
	table4.clear() ;
	alltable.clear() ;
	for( int i = 0; i< 100 ; i++ ){
		table5[i].folder = NULL ;
		table5[i].site = NULL ;
		table5[i].instruction = "" ;
	}
	for( int i = 0; i< 100 ; i++ ){
		table6[i].folder = NULL ;
		table6[i].site = NULL ;
		table6[i].instruction = "" ;
	}
	for( int i = 0; i< 100 ; i++ ){
		table7[i].folder = NULL ;
		table7[i].site = NULL ;
		table7[i].instruction = "" ;
	}
	
}


int main() {
  Mission final;
  int command = 0;
  string filename;
  
  do {
  	cout << endl << "************    SP Homework1    ************";
  	cout << endl << "* 0. QUIT                                  *";
  	cout << endl << "* 1. Get Token & output file               *";
  	cout << endl << "********************************************";
  	cout << endl << "Input a choice(0, 1): " ;
  	cin >> command;
  	switch( command ) {
  		case 0: return true;
  		case 1: {
  			final.readtable();
	  		final.readtxt() ;
	  		final.cutoken() ;
	  		final.clear() ;
			break;
		} // case1

		default: {
			cout << "Command does not exist! please try again" << endl ; 

		} // default
  		
	} // switch
  	
  } while(true);
  
  return 0 ;
} 

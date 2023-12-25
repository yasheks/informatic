#include <iostream>
#include<string>
#include "middle_str.h"
using namespace std;
long long len(string str)
{
     int i = 0;
    while(str[i] != '\0')
    {
        i++;
    }

    return i;
}
bool word(string a)
{
    int i =0;
    bool da;
    while(a[i] != '\0')
    {
        if(a[i] >= 'A' && a[i] <= 'z' || a[i] >= 'À' && a[i] <= 'ÿ' || a[i] == ' ') da = true;
        else return false;
        i++;
    }
    if(da)return true;
}
bool itc_isDigit(unsigned char c)
{
    if(c>='0' && c<='9') return true;
    else return false;
}
unsigned char itc_toUpper(unsigned char c)
{
    if (c<='z' && c >= 'a') return c - 32;
    else return c;
}
unsigned char itc_changeCase(unsigned char c)
{
    if (c<='Z' && c >= 'A') return c + 32;
    else itc_toUpper(c);
}
bool itc_compare(string s1, string s2)
{
    if(len(s1) != len(s2)) return false;
    else{
        for (int i=0;i<len(s1); i++)
        {
            if (s1[i] != s2[i]) return false;
        }
        return true;
    }
}
int itc_countWords(string str)
{
    int i = 0, score = 0;
    string strNew = "";
    bool broke = true;
    while (str[i] != '\0')
    {

        while (str[i] != ' ' && str[i] != '\0')
        {

            strNew += str[i];
            i++;
        }
        if (word(strNew))
        {
            score++;
        }
        else
        {
            broke = true;
        }
        if (str[i] != '\0')
        {
            i++;
            strNew = "";
        }
    }
    return score;
}
string itc_maxCharWord(string str)
{
    string strNew = "";
    bool yes;
    for (int i=0; i<len(str); i++)
    {
        if(str[i] == ' ') yes = true;
    }
    if(!yes) return "error";
    str ="n " + str + " e";

    int i = 0, score = 0;
    string bigstr="";
    bool broke = true;
    while (str[i] != '\0')
    {
        strNew += str[i];
        i+= 2;
        if (str[i] == ' ' or str[i] == ',')
        {
            i++;
            if(word(strNew))
            {
                if(len(bigstr) <= len(strNew))
                {
                    bigstr = strNew;
                    strNew = "";
                }
            }
        }

    }
    return bigstr;
}
char itc_sameChar(string str)
{
    int sovp = 2;
    for (int i =0; i<len(str); i++)
    {
        sovp = 2;
        for(int j = 0; j<len(str); j++)
        {
            if(str[j] == str[i] && str[str[j]!= ' ']){
                sovp--;
                if(sovp == 0) return str[j];
            }
        }
    }

}
bool itc_isFirstInSecond(string s1, string s2) {
        if (len(s1) > len(s2)) {
        return false;
        }

    for (int i = 0; i <= len(s2) - len(s1); i++) {
        bool isEqual = true;
        for (int j = 0; j < len(s1); j++) {
            if (s1[j] != s2[i + j]) {
                isEqual = false;
                break;
            }
        }

        if (isEqual) {
            return true;
        }
    }

    return false;
}
string itc_Cezar(string str, int k)
{
    string result = "";
    char small = 'a', full = 'z';
    if (k == 0) return str;
    for (int i = 0; i < str.length(); i++)
    {
        if (str[i] >= 'a' && str[i] <= 'z')
        {
            small = 'a';
            full = 'z';
        }
        else if (str[i] >= 'A' && str[i] <= 'Z')
        {
            small = 'A';
            full = 'Z';
        }
        else return "please enter the char a-Z";
        if(k>0)
        {
            if (str[i] + k > full)str[i] = small + (str[i] + k - full - 1);
            else str[i] += k;
        }
        else if (k < 0)
        {
            if (str[i] - k < small) str[i] = full +k-1;
            else str[i] += k;
        }

    }
    return str;
}
string itc_rmFreeSpace(string str)
{
    string result = "";
    for(int i =0; i<len(str); i++)
    {
        if(str[i] == ' ' && str[i+1] == ' ') continue;
        else result += str[i];
    }
    return result;
}
bool itc_isIp(string str)
{
    string strnew ="";
    int num = 0;

    if(str[0] == '.' || str[len(str)-1] == '.') return false;
    for(int i; i<len(str); i++)
    {
        while(str[i] != '.')
        {
            strnew += str[i];
            i++;
        }
        if(len(strnew) > 3) return false;
        for (char c : strnew)  num = num * 10 + (c - '0');
        if(num < 0 || num > 255) return false;
        num = 0;
        strnew = "";
    }
    return true;
}

//65-90
//97-122

/*string itc_Cezar(string str, int k) {
    string result = "";
    if (k == 0) return str;
    for (int i = 0; i < len(str); i++) {

        if (k > 0) {

            if (str[i] >= 'a' && str[i] <= 'z') {
                result += (str[i] - 'a' + k) % 26 + 'a';
            }

            else if (str[i] >= 'A' && str[i] <= 'Z') {
                result += (str[i] - 'A' + k) % 26 + 'A';
            }
        }

        else if (k < 0) {

            if (str[i] >= 'a' && str[i] <= 'z') {
                result += (str[i] - 'a' - k * (-1)) % 26 + 'a';
            }

            else if (str[i] >= 'A' && str[i] <= 'Z') {
                result += (str[i] - 'A' - k * (-1)) % 26 + 'A';
            }
        }
    }

    return result;
}
*/

# 스킬트리
- - - 

```
#include <string>
#include <vector>
#include <iostream>
using namespace std;
int possible = 1; //0이면 불가능 1이면 가능
int solution(string skill, vector<string> skill_trees) {
    int answer = 0;
    
    vector<string>::iterator it = skill_trees.begin();
    int skill_length = skill.length();
    
    for(it; it!=skill_trees.end(); it++){
        possible = 1;
        int *pos_of_skill = new int[skill.length()];
        for(int j=0; j<skill.length(); j++){
            pos_of_skill[j] = -100;
        }
        
        string current = *it;
        // skilltree에서 skill에 해당하는 문자열들의 위치를 찾아서 pos_of_skill에 저장한다. 
        for(int i=0; i<skill.length(); i++){ // skill 하나씩
            for(int k=0; k<current.length(); k++){  // 스킬트리에서 위치를 찾는다.
                // 못찾으면 -1을 반환하는 find 함수
                pos_of_skill[i] = current.find(skill[i]);
            }
        }
         for(int i=0; i<skill.length(); i++){
            cout << pos_of_skill[i] << " ";
        }
        cout << endl; 
        
        // pos_of_skill을 보면서 각 안되는 이유를 찾는다. 안되는 이유가 없다면 진행
        for(int m = 0; m<skill.length()-1; m++){
            if(pos_of_skill[m] == -1 && pos_of_skill[m+1] != -1){
                cout << "선행 스킬 배우질 않음. 안됨" << endl;
                possible = 0;
                break;
            }
            if(pos_of_skill[m] == -1 || pos_of_skill[m+1] == -1){
                continue;
            }
            if(pos_of_skill[m] != -1 && pos_of_skill[m+1] != -1 && pos_of_skill[m+1] < pos_of_skill[m]){
                cout << "뒤에꼐 먼저 배움, 안됨" << endl;
                possible = 0;
                break;
            }
            possible = 1;
        }
        if(possible == 1 ) {
            cout << "답이 됨" << endl;
            answer++;
        }
    }  
   
    return answer;
}
```

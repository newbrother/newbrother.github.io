---
layout: post
title: '[Codeforces] Round574(div2) : D1 - Submarine in the Rybinsk Sea (easy edition)'
---

[Round574(div2) : D1 - Submarine in the Rybinsk Sea (easy edition)](http://codeforces.com/contest/1195/problem/D1)

## 풀이

그리디

이문제의 포인트는 다른 숫자들과 상관없이 그리디한 값을 쉽게 찾을 수 있다는 것이다.

시간에 쫓겨 풀다가 결국 제출에는 실패하고, 바로 규칙을 찾아냈다.

input : 3
12, 33, 45 라면

12는 자기자신, 33, 45와 합쳐지므로

1122,1323,1425가 된다.

이때 D1(easy)에서는 숫자가 고정이므로 다른숫자와 상관없이

12라는 값에서 1은 1000의자리(자리수*2)에서 3번(n값)이 등장하고, 

100의자리에서 3번( n번(12에서 1번, 33에서 1번, 45에서 1번)) 등장한다.

마찬가지로 일의자리(두번째숫자) 2는 10의자리에서 3번, 1의자리에서 3번 등장한다.

따라서 1000*3 + 100*3 + 2*10*3 + 2*3 으로 바로 계산이 가능하다.

자리수 계산하는게 약간 까다로웠는데, 나는 그냥 귀찮아서 string으로 만들고는 0을 푸쉬했다.

테스트케이스에 나와있는 숫자가 굉장히 커서 long long으로는 overflow가 나는데,

계산해보니 unsinged long long으로는 overflow가 안나길래 이 타입으로 계산했고,

stoull를 이용해서 문자열에서 ull로 변경하게끔 풀었다.

그리고 모듀럴 연산을 ans값을 꺼내서 계속 먹여줘야하는것도 잊지 않았다.

풀고나니까 너무 삽질 한것같았다.

각자리수 별로 메모이제이션을 쭉해서 숫자를 더한다음에 n과 자리수를 곱하는 방법도 떠올랐다.

그래서 다른 사람 풀이를 찾아보니까 자리수 계산후 10씩 계속해서 곱해주는 방식으로 푸셨더라

(밑에 첨부해놨음) 앞으로도 이렇게 직관적이고 간결하게 짜도록 노력해야겠다.


## 코드

내코드

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>
#include <cstring>
#include <string>
#include <queue>
#include <map>
using namespace std;

int arr[100000];
const int mo = 998244353;

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    string s = to_string(arr[0]);
    int size = s.size();
    unsigned long long ans = 0;
    for (int i = 0; i < n; i++) {
        s = to_string(arr[i]);
        for (int j = 0; j < size; j++) {
            if (s[j] == '0')
                continue;
            string tmp;
            tmp.push_back(s[j]);
            for (int k = 0; k < (size - j) * 2 - 1; k++) {
                tmp.push_back('0');
            }
            unsigned long long tmpNum = stoull(tmp);
            tmpNum += tmpNum / 10;
            ans = (ans + (tmpNum%mo * n )%mo)%mo;
        }
    }
    cout << ans;
    return 0;
}
```

더간단하게푸신분 코드(속도도 빠름)

```cpp
#include <iostream>
using namespace std;
#define mod 998244353
long long ans=0;
long long now=0;
int main() {
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        scanf("%lld",&now);
        int cnt=0;
        long long tmp=now;
        int num[15];
        while(tmp)
        {
            num[cnt]=tmp%10;
            cnt++;
            tmp/=10;
        }
        long long t=now;
        long long sum=0;
        for(int i=cnt-1;i>=0;i--)
        {
            sum=sum*10+num[i];
            sum%=mod; 
            sum=sum*10+num[i];
            sum%=mod; 
        }
 
        ans=(ans+sum*n)%mod;
    }
    cout<<ans<<endl;
}
```

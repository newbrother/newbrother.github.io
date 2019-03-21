---
layout: post
title: '[Codeforces] Round547(div3) : D - Colored Boots'
---

[Round547(div3) : D - Colored Boots](http://codeforces.com/contest/1141/problem/D)

## 풀이

구현

알파벳이 V1,v2 두군데 모두 있으면 먼저 처리하고,

그후에 v1의 ? 개수만큼 v2의 아무 알파벳과 처리하고,

v2의 ? 개수만큼 v1의 아무 알파벳과 처리하고,

마지막으로 v1,v2의 남은 ?끼리 짝지어주면 된다.


## 코드

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    int n;
    cin >> n;
    string str1, str2;
    cin >> str1 >> str2;

    //a:0 ~z:25, ?:
    vector<int> v[27];
    vector<int> v2[27];
    for (int i = 0; i<str1.size(); i++) {
        if (str1[i] == '?') {
            v[26].push_back(i + 1);
        }
        else {
            v[str1[i] - 'a'].push_back(i + 1);
        }
    }
    for (int i = 0; i<str2.size(); i++) {
        if (str2[i] == '?') {
            v2[26].push_back(i + 1);
        }
        else {
            v2[str2[i] - 'a'].push_back(i + 1);
        }
    }
    vector<pair<int, int>> vp;
    int ans = 0;
    for (int i = 0; i<26; i++) {
        while (v[i].size()>0 && v2[i].size()>0) {
            vp.push_back({ v[i].back(),v2[i].back() });
            v[i].pop_back();
            v2[i].pop_back();
            ans++;
        }
    }
    //물음표처리 v1 ? ->v2 단어 ,  v2 ? -> v1 단어, v1 ? <-> v2 ?
    int i = 0;
    while (v[26].size()>0) {
        if (i == 26)
            break;
        while (v2[i].size()>0 && v[26].size()>0) {
            vp.push_back({ v[26].back(),v2[i].back() });
            v[26].pop_back();
            v2[i].pop_back();
            ans++;
        }
        i++;
    }
    i = 0;
    while (v2[26].size()>0) {
        if (i == 26)
            break;
        while (v[i].size()>0 && v2[26].size()>0) {
            vp.push_back({ v[i].back(),v2[26].back() });
            v[i].pop_back();
            v2[26].pop_back();
            ans++;
        }
        i++;
    }
    while (v[26].size()>0 && v2[26].size()>0) {
        vp.push_back({ v[26].back(),v2[26].back() });
        v[26].pop_back();
        v2[26].pop_back();
        ans++;
    }

    cout << ans << '\n';
    for (int i = 0; i<ans; i++) {
        cout << vp[i].first << ' ' << vp[i].second << '\n';
    }
    return 0;
}
```

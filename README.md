## PS & CF
[![Solved.ac
프로필](http://mazassumnida.wtf/api/mini/generate_badge?boj=zlfn)](https://solved.ac/zlfn)
[![Codeforces](https://badges.joonhyung.xyz/codeforces/zlfn.svg)](https://codeforces.com/profile/zlfn)
[![AtCoder](https://badges.joonhyung.xyz/atcoder/zlfn.svg)](https://atcoder.jp/zlfn/topology)

## First, solve the problem. Then, write the code.
### [Beakjoon Online Judge](boj.kr) ||  [Solved.ac](solved.ac)

[![Solved.ac
프로필](http://mazassumnida.wtf/api/v2/generate_badge?boj=zlfn)](https://solved.ac/zlfn)
![mazandi profile](http://mazandi.herokuapp.com/api?handle=zlfn&theme=cold)
---------------------------
### [Codeforces](codeforces.com)
[![Codeforces](https://badges.joonhyung.xyz/codeforces/zlfn.svg)](https://codeforces.com/profile/zlfn)  
![](https://raw.githubusercontent.com/zlfn/cf-stats/main/output/light_card.svg)
[![CodeForces Profile](https://cf.leed.at?id=zlfn)](https://codeforces.com/profile/zlfn)
--------------------------
### [AtCoder](atcoder.jp)
[![AtCoder](https://badges.joonhyung.xyz/atcoder/zlfn.svg)](https://atcoder.jp/zlfn/topology)  
엣코더 스텟카드는 못찾았음...
--------------------------
### C++ PS 프리셋 (v1.2, 2024.04.06)
#### 주요 기능
* MMAP을 이용한 빠른 입출력 (linux 환경에서만 활성화, #define MMAP 주석해제 필요)
* debug 출력 제공 (cout과 사용법은 동일하나 온라인저지 환경에서 미출력)
* loop, loopi, cinloop, cinloopi 매크로
* llint 매크로
* streamIO 매크로 (nn, nm, endl, nendl, nendln, spc, nspc, nspcn, coutn, cinn, coutnendl, coutnspc)
* 변수 선언 및 입력 매크로 (cinint ... cinstring)

```cpp
#include <bits/stdc++.h>
//#define MMAP
using namespace std;
//////////////////////////////////////////////////////////////////
#ifdef __linux__
/////////////////////////////////////////////////////////////////////////////////////////////
/*
 * Author : jinhan814
 * Date : 2021-05-06
 * Source : https://blog.naver.com/jinhan814/222266396476
 * Description : FastIO implementation for cin, cout.
 */
constexpr int SZ = 1 << 20;

class INPUT {
private:
    char read_buf[SZ];
    int read_idx, next_idx;
    bool __END_FLAG__, __GETLINE_FLAG__;
public:
    explicit operator bool() { return !__END_FLAG__; }
    bool IsBlank(char c) { return c == ' ' || c == '\n'; }
    bool IsEnd(char c) { return c == '\0'; }
    char _ReadChar() {
        if (read_idx == next_idx) {
            next_idx = fread(read_buf, sizeof(char), SZ, stdin);
            if (next_idx == 0) return 0;
            read_idx = 0;
        }
        return read_buf[read_idx++];
    }
    char ReadChar() {
        char ret = _ReadChar();
        for (; IsBlank(ret); ret = _ReadChar());
        return ret;
    }
    template<typename T> T ReadInt() {
        T ret = 0; char cur = _ReadChar(); bool flag = 0;
        for (; IsBlank(cur); cur = _ReadChar());
        if (cur == '-') flag = 1, cur = _ReadChar();
        for (; !IsBlank(cur) && !IsEnd(cur); cur = _ReadChar()) ret = 10 * ret + (cur & 15);
        if (IsEnd(cur)) __END_FLAG__ = 1;
        return flag ? -ret : ret;
    }
    string ReadString() {
        string ret; char cur = _ReadChar();
        for (; IsBlank(cur); cur = _ReadChar());
        for (; !IsBlank(cur) && !IsEnd(cur); cur = _ReadChar()) ret.push_back(cur);
        if (IsEnd(cur)) __END_FLAG__ = 1;
        return ret;
    }
    double ReadDouble() {
        string ret = ReadString();
        return stod(ret);
    }
    string getline() {
        string ret; char cur = _ReadChar();
        for (; cur != '\n' && !IsEnd(cur); cur = _ReadChar()) ret.push_back(cur);
        if (__GETLINE_FLAG__) __END_FLAG__ = 1;
        if (IsEnd(cur)) __GETLINE_FLAG__ = 1;
        return ret;
    }
    friend INPUT& getline(INPUT& in, string& s) { s = in.getline(); return in; }
} _in;

class OUTPUT {
private:
    char write_buf[SZ];
    int write_idx;
public:
    ~OUTPUT() { Flush(); }
    explicit operator bool() { return 1; }
    void Flush() {
        fwrite(write_buf, sizeof(char), write_idx, stdout);
        write_idx = 0;
    }
    void WriteChar(char c) {
        if (write_idx == SZ) Flush();
        write_buf[write_idx++] = c;
    }
    template<typename T> int GetSize(T n) {
        int ret = 1;
        for (n = n >= 0 ? n : -n; n >= 10; n /= 10) ret++;
        return ret;
    }
    template<typename T> void WriteInt(T n) {
        int sz = GetSize(n);
        if (write_idx + sz >= SZ) Flush();
        if (n < 0) write_buf[write_idx++] = '-', n = -n;
        for (int i = sz; i-- > 0; n /= 10) write_buf[write_idx + i] = n % 10 | 48;
        write_idx += sz;
    }
    void WriteString(string s) { for (auto& c : s) WriteChar(c); }
    void WriteDouble(double d) { WriteString(to_string(d)); }
} _out;

/* operators */
INPUT& operator>> (INPUT& in, char& i) { i = in.ReadChar(); return in; }
INPUT& operator>> (INPUT& in, string& i) { i = in.ReadString(); return in; }
template<typename T, typename std::enable_if_t<is_arithmetic_v<T>>* = nullptr>
INPUT& operator>> (INPUT& in, T& i) {
    if constexpr (is_floating_point_v<T>) i = in.ReadDouble();
    else if constexpr (is_integral_v<T>) i = in.ReadInt<T>(); return in; }

OUTPUT& operator<< (OUTPUT& out, char i) { out.WriteChar(i); return out; }
OUTPUT& operator<< (OUTPUT& out, string i) { out.WriteString(i); return out; }
template<typename T, typename std::enable_if_t<is_arithmetic_v<T>>* = nullptr>
OUTPUT& operator<< (OUTPUT& out, T i) {
    if constexpr (is_floating_point_v<T>) out.WriteDouble(i);
    else if constexpr (is_integral_v<T>) out.WriteInt<T>(i); return out; }

/* macros */
#define fastio 1
#define cin _in
#define cout _out
/////////////////////////////////////////////////////////////////////////////////////////////
#endif

//util
#define llint long long int
#define endl '\n'
#define nendl << '\n'
#define nendln << '\n' <<
#define nn <<
#define nm >>
#define spc ' '
#define nspcn << ' ' <<
#define nspc << ' '
#define cinn cin >>
#define cinint(x) int x; cin >> x
#define cinllint(x) long long int x; cin >> x
#define cinchar(x) char x; cin >> x
#define cinfloat(x) floag x; cin >> x
#define cindouble(x) double x; cin >> x
#define cinstring(x) string x; cin >> x
#define coutn cout <<
#define coutnendl cout nendl
#define coutnspc cout nspc
#define loop(x) for(int IDX = 0; IDX < x; IDX++)
#define loopi(x, i) for(int i = 0; i < x; i++)
#define cinloop cinint(INDEX); loop(INDEX)
#define cinloopi(i) cinint(IDX##i); loopi(IDX##i, i)

//debug
#define debug if constexpr (DEBUGENV) cout
#define debugn debug <<
#define debugnendl debug << endl;
#ifdef ONLINE_JUDGE
constexpr bool DEBUGENV = false;
#else
constexpr bool DEBUGENV = true;
#endif

//FASTIO
#define FASTIO debugn "LOW-LEVEL-IO Enabled" nendl;
#ifndef MMAP
#undef cin
#undef cout
#undef FASTIO
#define FASTIO debugn "FAST-IO Enabled" nendl; ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL)
#endif

/////////////////////////////////////////////////////////////////////
```

### Rust PS 프리셋 (v1.0, 2024.04.04)
#### 주요 기능
* Rust의 거지같은 표준입출력을 간략하게 만듬

```rs
use std::io;

macro_rules! read_line {
    ($($t: ty),+) => ({
        let mut input = String::new();
        std::io::stdin().read_line(&mut input).unwrap();
        let mut iter = input.split_whitespace();
        ($(iter.next().unwrap().parse::<$t>().unwrap()),+)
    })
}

macro_rules! read_vec {
    ($t: ty) => ({
        let mut input = String::new();
        std::io::stdin( ).read_line(&mut input).unwrap();
        input.split_whitespace().map(|x| x.parse::<$t>().unwrap()).collect()
    })
}

macro_rules! read_char {
    () => ({
        let mut input = String::new();
        std::io::stdin().read_line(&mut input).unwrap();
        input = input.replace("\n", "");
        input.chars().collect()
    })
}
```

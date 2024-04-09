## PS & CF
[![Solved.ac
프로필](http://mazassumnida.wtf/api/mini/generate_badge?boj=zlfn)](https://solved.ac/zlfn)
[![Codeforces](https://badges.joonhyung.xyz/codeforces/zlfn.svg)](https://codeforces.com/profile/zlfn)
[![AtCoder](https://badges.joonhyung.xyz/atcoder/zlfn.svg)](https://atcoder.jp/zlfn/topology)

## First, solve the problem. Then, write the code.

## C++ PS 프리셋 (v1.2, 2024.04.06)
**C++17 이상**
<details>
<summary>코드 열기</summary>
    
```cpp
#include <bits/stdc++.h>
#define DEBUG true //PRINT DEBUG MESSAGE
#define MMAP false //USE LOW-LEVEL-IO
using namespace std;
//////////////////////////////////////////////////////////////////
/*
 * Author : zlfn
 * Date : 2024-04-08
 * Source : https://ps.zlfn.space
 * Description : C++ Preset for Problem-Solving
 */
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
#if DEBUG && not defined(ONLINE_JUDGE)
constexpr bool DEBUGENV = true;
#else
constexpr bool DEBUGENV = false;
#endif

//FASTIO
#define FASTIO debugn "LOW-LEVEL-IO Enabled" nendl;
#if not MMAP
#undef cin
#undef cout
#undef FASTIO
#define FASTIO debugn "FAST-IO Enabled" nendl; ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL)
#endif
/////////////////////////////////////////////////////////////////////
```
    
</details>

### 주요 기능
#### FAST/LOW-LEVEL-IO
* MMAP을 이용한 빠른 입출력 (linux 환경에서만 활성화, #define MMAP true 필요)
#### Debug
* debug 출력 제공 (cout과 사용법은 동일하나 온라인저지 환경에서 미출력)
#### Util
* loop, loopi, cinloop, cinloopi 매크로
* llint 매크로
* streamIO 매크로 (nn, nm, endl, nendl, nendln, spc, nspc, nspcn, coutn, cinn, coutnendl, coutnspc)
* 변수 선언 및 입력 매크로 (cinint ... cinstring)

## C++ Geometry Extension (v0.1, 2024.04.10)
**C++20 이상, 기본 Preset 필수**
<details>
    <summary>코드 열기</summary>
    
```cpp
//////////////////////////////////////////////////////////////////
class Point {
public:
    int x; int y;
    Point() {
        x = 0; y = 0;
    }
    Point(int x, int y) {
        this->x = x; this->y = y;
    }
    double operator <=> (const Point& other) const {
        return sqrt(pow(x-other.x,2) + pow(y-other.y,2));
    }
    Point operator - (const Point& other) const {
        return Point{x-other.x, y-other.y};
    }
    Point operator + (const Point& other) const {
        return Point{x+other.x, y+other.y};
    }
    bool operator == (const Point& other) const {
        return (x==other.x && y==other.y);
    }
};
//////////////////////////////////////////////////////////////////
```
</details>

### 주요 기능
#### Class
* 2차원 정점 Point `+, -, ==, <=> (거리)` 연산 제공

## Rust PS 프리셋 (v1.0, 2024.04.04)
<details>
<summary>코드 열기</summary>

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
    
</details>

### 주요 기능
* Rust의 거지같은 표준입출력을 간략하게 만듬

-----------------------------------

#### [Beakjoon Online Judge](boj.kr) ||  [Solved.ac](solved.ac)

[![Solved.ac
프로필](http://mazassumnida.wtf/api/v2/generate_badge?boj=zlfn)](https://solved.ac/zlfn)
![mazandi profile](http://mazandi.herokuapp.com/api?handle=zlfn&theme=cold)
---------------------------
#### [Codeforces](codeforces.com)
[![Codeforces](https://badges.joonhyung.xyz/codeforces/zlfn.svg)](https://codeforces.com/profile/zlfn)  
![](https://raw.githubusercontent.com/zlfn/cf-stats/main/output/light_card.svg)
[![CodeForces Profile](https://cf.leed.at?id=zlfn)](https://codeforces.com/profile/zlfn)
--------------------------
#### [AtCoder](atcoder.jp)
[![AtCoder](https://badges.joonhyung.xyz/atcoder/zlfn.svg)](https://atcoder.jp/zlfn/topology)  
[![zlfn's atcoder stats](https://atcoder-readme-stats.vercel.app/stats/zlfn?show_icons=true&show_history=5&width=450)](https://atcoder.jp/zlfn/topology)
--------------------------


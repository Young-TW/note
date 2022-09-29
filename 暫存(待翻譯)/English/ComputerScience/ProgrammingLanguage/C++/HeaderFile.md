---
tags: Note
---

# C++ Header File

[TOC]

## Introduction

## include

### Concept of include

### Usage

Use this method to include header files in `C++`。  

```cpp
#include <>
#include ""
```

## Write header file

### Example

```h
#ifndef ADD_H
#define ADD_H

int add(int, int);

#endif
```

 <!-- 參考 https://zh.wikipedia.org/zh-tw/%E5%A4%B4%E6%96%87%E4%BB%B6 -->

## Content of Header File

### Class

See [Class.md](Class.md) for more detail.

### Namespace

See [Namespace.md](Namespace.md) for more detail.

### Function

See [Function.md](Function.md) for more detail.

## bits/stdc++.h

### Introduction

Some people use `C++` to solve problem on Online-Judge often use this line.
`#include <bits/stdc++.h>`  
This line can include all `C++` header files in one line.  
It's very convenient to them.
But normal developer usually not use this for develop.  

### Usage

要注意的是編譯器有沒有支援這個寫法，
像是 `Windows` 預設的 `C++` 編譯器就不支援，
不過大部分 `Online Judge` 或是試場的編譯器都會支援。

#### Example

```cpp
#include <bits/stdc++.h>
```

### 無法使用萬用標頭檔的替代方案

如果編譯器不支援的話也可以新增一個資料夾叫做 `bits`，
接著在資料夾內建立檔案 `stdc++.h`，
貼上下面的萬用標頭檔內容進 `stdc++.h`，
再使用以下方法：  

#### Example

```cpp
#include "bits/stdc++.h"
```

### content of bits/stdc++.h

```h
// C++ includes used for precompiling -*- C++ -*-

// Copyright (C) 2003-2014 Free Software Foundation, Inc.
//
// This file is part of the GNU ISO C++ Library.  This library is free
// software; you can redistribute it and/or modify it under the
// terms of the GNU General Public License as published by the
// Free Software Foundation; either version 3, or (at your option)
// any later version.

// This library is distributed in the hope that it will be useful,
// but WITHOUT ANY WARRANTY; without even the implied warranty of
// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
// GNU General Public License for more details.

// Under Section 7 of GPL version 3, you are granted additional
// permissions described in the GCC Runtime Library Exception, version
// 3.1, as published by the Free Software Foundation.

// You should have received a copy of the GNU General Public License and
// a copy of the GCC Runtime Library Exception along with this program;
// see the files COPYING3 and COPYING.RUNTIME respectively.  If not, see
// <http://www.gnu.org/licenses/>.

/** @file stdc++.h
 *  This is an implementation file for a precompiled header.
 */

// 17.4.1.2 Headers

// C
#ifndef _GLIBCXX_NO_ASSERT
#include <cassert>
#endif
#include <cctype>
#include <cerrno>
#include <cfloat>
#include <ciso646>
#include <climits>
#include <clocale>
#include <cmath>
#include <csetjmp>
#include <csignal>
#include <cstdarg>
#include <cstddef>
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <ctime>

#if __cplusplus >= 201103L
#include <ccomplex>
#include <cfenv>
#include <cinttypes>
#include <cstdalign>
#include <cstdbool>
#include <cstdint>
#include <ctgmath>
#include <cwchar>
#include <cwctype>
#endif

// C++
#include <algorithm>
#include <bitset>
#include <complex>
#include <deque>
#include <exception>
#include <fstream>
#include <functional>
#include <iomanip>
#include <ios>
#include <iosfwd>
#include <iostream>
#include <istream>
#include <iterator>
#include <limits>
#include <list>
#include <locale>
#include <map>
#include <memory>
#include <new>
#include <numeric>
#include <ostream>
#include <queue>
#include <set>
#include <sstream>
#include <stack>
#include <stdexcept>
#include <streambuf>
#include <string>
#include <typeinfo>
#include <utility>
#include <valarray>
#include <vector>

#if __cplusplus >= 201103L
#include <array>
#include <atomic>
#include <chrono>
#include <condition_variable>
#include <forward_list>
#include <future>
#include <initializer_list>
#include <mutex>
#include <random>
#include <ratio>
#include <regex>
#include <scoped_allocator>
#include <system_error>
#include <thread>
#include <tuple>
#include <typeindex>
#include <type_traits>
#include <unordered_map>
#include <unordered_set>
#endif
```
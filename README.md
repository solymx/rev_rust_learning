# rev_rust_learning


## IDA Pro

- 看到 main() 並不是實際的 main ，main 會被放在裡面，要一路追進去
- 有些有註解寫 `// main.rs` 這才是真的 `main()` ，可以直接 `alt + t` 來找

### start() 入口

export -> start 進去看，裡面是一堆準備的程式碼，但最下面一般會有一個 Code = xxx ，這個 Code 會接到最下面的 `exit()` 是的話他就是 `main()`

```
  Code = sub_42DA60(dword_588024, dword_588020);
  Code = Code;
  if ( !dword_588014 )
    exit(Code);
  if ( !dword_588010 )
  {
    cexit();
    return Code;
  }
  return Code;
}
```

上述的 main 就是 `sub_42DA60`，但他也不算是真正意義上的 main() ，裡面還是一堆準備工作，只是他是下一個做事的函數而已

進去上述為底下

```
int __usercall sub_42DA60@<eax>(int a1@<eax>)
{
  void *v2; // [esp+0h] [ebp-Ch] BYREF

  sub_4FA410(a1);
  v2 = &sub_4261C0; // 把 sub_4261C0 的「地址」存到 v2 變數裡
  return sub_4C2780(&v2, &off_516064); // 呼叫 Rust 執行環境的啟動函式
}
```

上面 a1 那個是做 wrapper ，一般都長那樣，之後 v2 是一個 function pointer 拿 sub_4261C0 並放到 return 那行的參數，所以這邊可以直接知道重點是 return 那行的 `sub_4C2780`

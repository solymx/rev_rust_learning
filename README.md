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

上述的 main 就是 `sub_42DA60`

# Bank Switching
Explicetly writing bank numbers are not a thing in Gaba. Instead you use Bank Groups to divide your rom into banked sections. All data inside a bank group is guaranteed to be placed in the same bank, thus you can safely reference labels between them. 

```
bankgroup "World Data" {

}

bankgroup "Overworld code" {
    
}

bankgroup "World Data" {
    
}

// Any bankgroup that is not "main" will be placed in a switchable bank
bankgroup "main" {
    main := main()
}
```

What about WRAM, SRAM, VRAM, and HRAM?




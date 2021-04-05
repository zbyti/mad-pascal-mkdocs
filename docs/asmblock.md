#

## ASM

Bloki assemblera nie są przez kompilator weryfikowane pod względem składni, dokonuje tego dopiero **Mad Assembler**.

Kompilator dopuszcza dwie składnie bloku `ASM`, z klamrami { } jak dla komentarza i standardową bez klamer

```delphi
ASM
  lda #10
  sta 712
END;
```

```delphi
ASM
{  lda #10
   sta 712
};
```

```delphi
procedure name; assembler;
asm
  lda #10
  sta 712
end;
```

```delphi
procedure name; assembler;
asm
{
  lda #10
  sta 712
};
end;
```

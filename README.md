# bash-exit-status

<h3>Exit Status</h3>
exit status / return code /exit code
range 0 - 255
0 = sucess (sikeres)
0-tól eltérő = valamilyen hiba állapot
Használj error checking-et!
Használj man vagy info parancsot, hogy megtaláld az exit status jelentését!


<h3>Exit Status ellenőrzése</h3>

<h4>PÉLDA:</h4>

```
ls /nincs/ilyen
echo "$?"
```

<h4>KIMENET:</h4>

```
2
```

<h3>Ping parancs</h3>

`ping -c 1`
A következőt jelenti:
`-c <count>` = count vagyis számláló (hányszor próbálkozzon a ping)
`-c 1` = 1 szer próbálja a pinget, utána álljon le

<h5>1. host-reachable.sh</h5>

```
HOST="google.com"

ping -c 1 $HOST

if [ "$?" -eq "0" ]
then
    echo $HOST reachable.
else
    echo $HOST unreachable.
fi
```

<h5>2. host-unreachable.sh</h5>

```
HOST="google.com"

ping -c 1 $HOST

if [ "$?" -ne "0" ]
then
    echo $HOST unreachable.
fi

```

<h5>3. return-code.sh<h5>

```
HOST="google.com"
ping -c 1 $HOST
RETURN_CODE=$?

echo $RETURN_CODE

```
| operátor | jelentés | példa |
|:-|:-|:-|
| && | AND | mkdir /tmp/bak && cp test.txt /tmp/bak |
| &#124; &#124;| OR | cp test.txt /tmp/bak &#124; &#124; cp test.txt /tmp |


*Az AND és OR használható IF helyett.*

**AND példa magyarázat:**
Ha az `mkdir /tmp/bak` lefut, akkor és csak akkor fut le a `cp test.txt /tmp/bak` is.

**OR példa magyarázat:**
Ha a `cp test.txt /tmp/bak` lefut, akkor a `cp test.txt /tmp` nem fut le.
Ha a `cp test.txt /tmp/bak` nem fut le, akkor lefut a `cp test.txt /tmp` .

<h3>Pontosvessző</h3>

- Nem ellenőrzi az exit code-ot.
- Ha több parancsot ; -vel szeparálunk, akkor mindenképp lefutnak, anélkül, hogy figyelembe vennék az előttük lévő exit code-ját.

<h3>Exit parancs</h3>
exit = kilépés
- Ha megadom az exit után az exit codeot 0-255 között, akkor azzal lép ki.
- Ha nem adom meg akkor az utolsó korábban lefutott parancs exit codeját örökli a `$?`.

<h3>Összegzés</h3>
- minden parancs visszaad egy exit status-t
- 0 - 255
- 0 = sikeres
- 0-tól eltérő = error condition
- `$?` változó tárolja az exit status-t
- elágazást lehet if-fel vagy &&-el / || -ral
- exit



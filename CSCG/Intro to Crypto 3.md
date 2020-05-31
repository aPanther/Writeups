# Intro to Crypto 3
**Category:** Crypto    
**Difficulty:** Baby  
**Author:** black-simon  
>This is an introductory challenge for beginners which want to dive into the world of Cryptography. The three stages of this challenge will increase in difficulty. 
After a new potentially deadly disease first occurring in Wuhan, China, the Chinese Corona Response Team sends messages to the remainder of the world. 
However, to avoid disturbing the population, they send out this message encrypted.   
We have intercepted all messages sent by the Chinese government and provide you with the public keys found on the governments' website.  Please, find out if we are all going to die!

## Solution
We are given three RSA public keys, and three ciphers encrypted using the given public keys. So, one message, encrypted three times using different keys but same exponent. Of course, the chinese remainder theorem.
We can obtain the original plain text message using the chinese remainder. According to CRT:
```
X ≡ a1 (mod n1)
X ≡ a2 (mod n2)
X ≡ a3 (mod n3)

N = n1*n2*n3
N1 = n2*n3
N2 = n1*n3
N3 = n1*n2

y1 = inv(N1)(mod n1)
y2 = inv(N2)(mod n2)
y3 = inv(N3)(mod n3)

X = (a1*N1*y1 + a2*N2*y2 + a3*N3*y3) (mod N)
```
In our case a1, a2 and a3 are ciphers, X is message**3. n1, n2 and n3 is modulus of three public keys. So we can find the cube of message with CRT and then the original message.
```python
Ng = 0x69E5E5DB6A80A32C59EC1EC63710F4886407EE0007A1050B22178D5AE88865D861B66371A93120D581BA701BC1221CF2B4A0E3F3FF15F79DFE66D0F7A795E9B083650F382FA5F7E5B4D8FD7A85423DEB8263F595701B9E863E3B698D3ED1629B9394580AB50C511C9A9C059F9B7C3F02BDEC1FBE4FA9B13A376F04245493727A19D32E820BA4AA31535CEE42CC4EC2603FFCE5D77255376A5BBD693F275618D8C0900EB4F4F263BEDAA524BD0FB650D59C7DEBA3DE4BFA4FB3CA50312FC585860E89C01BD90675F321CC7EDC83912E9E3A9590FF08B145851B1CF847BD2BAF1A4A6D409E8BBB8ECD374743C65FCEAF052C33A430670770ABF24DAEEA2F276F67
Nr = 0x914F6B95335685BA37F4F95BF9893ED7C02BB131D6D7A4A37CED72C31F5283A65774EA67D38C7029D1E751A82564B2C189BF6C76C75E07F8738E973636856F3461D59211FE96F818A4193A0AD4532CC1E595FF187DC8CE1490AD19AE9E4B2EA63A070EE7E92D436C6452FA07007E3A9662EEEB432AE90354A0749C3FCA8FA5E25EA73D640C352E165A857CEFA1628AFA17E024B73E78246E12402E71AB65ABBEDCED8306629D31194AD88BF07B085ABE723500FD02E44E7042079CFB8158C6ED88B7DFD25266E4199F68ED1C582FD959F87A572F7AB8C7B54EF327205F710C7F270B229DD7A37315582E5921865ADC7B74AC73816BE21B42E0BDD9117E2FB133
Nu = 0x7292F12B97F2BB6810AB6DE8C12B114015248A38FD516BF51A58E6A3443A4B705806253D709E70DE0B567AE3B1DC012239EE518AFB9B3623140055A8BD3A30254EA4998743BBB0EDF1129C40E098CE28107F36D31776B2F153142CAF79E325E47808F6F5CFDDDF56247A2AC289A5BFC20BA723BA8B5AD26DF7A9658F824E8509C325362FC8CD304F723F33EBF0B065C6D60B2B9B9D33EF0B39CE41B1C7E3AF547F6D0F65CA7FB41228271BB7DCAF8B707F941751EB85A7D2C58578E11215D301CD72C0D1917F12E151595EE3FE408A7549D9E986E58254951410E4EDD1D88F3776DF3293C8355B3CDBF37B26DB838D2046AA18628851DFC6883E1736C0EFABA3
N = Nu * Ng * Nr
Mg = Nu * Nr
Mr = Nu * Ng
Mu = Nr * Ng
e = 3
cipherg = 3999545484320691620582760666106855727053549021662410570083429799334896462058097237449452993493720397790227435476345796746350169898032571754431738796344192821893497314910675156060408828511224220581582267651003911249219982138536071681121746144489861384682069580518366312319281158322907487188395349879852550922320727712516788080905540183885824808830769333571423141968760237964225240345978930859865816046424226809982967625093916471686949351836460279672029156397296634161792608413714942060302950192875262254161154196090187563688426890555569975685998994856798884592116345112968858442266655851601596662913782292282171174885
cipheru = 7156090217741040585758955899433965707162947606350521948050112381514262664247963697650055668324095568121356193295269338497644168513453950802075729741157428606617001908718212348868412342224351012838448314953813036299391241983248160741119053639242636496528707303681650997650419095909359735261506378554601448197330047261478549324349224272907044375254024488417128064991560328424530705840832289740420282298553780466036967138660308477595702475699772675652723918837801775022118361119700350026576279867546392616677468749480023097012345473460622347587495191385237437474584054083447681853670339780383259673339144195425181149815
cipherr = 9343715678106945233699669787842699250821452729365496523062308278114178149719235923445953522128410659220617418971359137459068077630717894445019972202645078435758918557351185577871693207368250243507266991929090173200996910881754217374691865096976051997491208921880703490275111904577396998775470664002942232492755888378994040358902392803421017545356248082413409915177589953816030273082416979477368273328755386893089597798104163894528521114946660635364704437632205696975201216810929650384600357902888251066301913255240181601332549134854827134537709002733583099558377965114809251454424800517166814936432579406541946707525

def multiplicative_inverse(a, b):
    x = 0
    y = 1
    lx = 1
    ly = 0
    oa = a  
    ob = b  
    while b != 0:
        q = a // b
        (a, b) = (b, a % b)
        (x, lx) = ((lx - (q * x)), x)
        (y, ly) = ((ly - (q * y)), y)
    if lx < 0:
        lx += ob  
    if ly < 0:
        ly += oa  
    return lx

invg = multiplicative_inverse(Mg,Ng)
invr = multiplicative_inverse(Mr,Nr)
invu = multiplicative_inverse(Mu,Nu)
text = cipherg * Mg * invg
text += cipherr * Mr * invr
text += cipheru * Mu * invu
text = text % N

def find_invpow(x,n):
    high = 1
    while high ** n < x:
        high *= 2
    low = high//2
    while low < high:
        mid = (low + high) // 2
        if low < mid and mid**n < x:
            low = mid
        elif high > mid and mid**n > x:
            high = mid
        else:
            return mid
    return mid + 1
    
message = find_invpow(text,3)
from Crypto.Util.number import long_to_bytes
print(long_to_bytes(message))
```
Running this python program, we get the flag.
```bash
$python3 crt.py 
b'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACSCG{ch1nes3_g0vernm3nt_h4s_n0_pr0blem_w1th_c0ron4}'
```
### CSCG{ch1nes3\_g0vernm3nt\_h4s\_0n\_pr0blem\_w1th\_c0ron4}
# SSS-Par2
Crypto Chall TimCTF


This challenge is the seconde SSS (Shamir Secret Sharing) challenge put on timctf [BTW thanks to the organizers ^^]
You can find attached here the different files provided with the task.


They used a 12° degree polynomiall, means we need 13 points to get the secret! but they provided only 10 points! (Here you start thinking of some bruteforcing)

In the description they say it was a personnal implementation so i digged  'sss.py' and realized that they were splitting the flag into 4 chunks, then encrypted each one alone! seems allright already!  But here was the vulnerability: they used the same Lagrange Polynomial coefficients (except for the secret S obviously).



What we exploit: the distance between two polynomials will be the same for all points! So knowing P(x), Q(x) and P(y) you can get Q(y)! because P(x) - Q(x) == P(y) - Q(y)

Well for the chunk0 polynomial we allready have the 10 given points associated with {1,2,5,6,7,11,12,14,15,16} 
[see 'shares.txt' file] 


Let p0,p1,p2,p3 the four polynomials and S0,S1,S2,S3 the four secrects associated respectively with chunk0, chunk1, chunk2 and chunk3


We know p0(1) and p1(1) and p1(4) then p0(1) - p1(1) == p0(4) - p1(4) implies p0(4) == p1(4) + (p0(1) - p1(1))

Yayyy another point for p0, still we have to gain knowledge on  2 other points.

Using the same methode with other points available in the different chunks we can get p0(9) ans p0(10) => we have now 13 points


I used an online website to calculate p0 and got S from p0(0) and we have the first chunk : 'timctf{d0_'


Using the same methode above we can get the other chunks (cause Si == pi(0)! makes sense?)

After calculating p1(0), p2(0) ans p3(0) we get our flag = 'timctf{d0_NOt_R3inV3nT_CrYpt0_Pl34sE}'

AND DO NOT REINVENT CRYPTO PLZ! (unless you know what you are doing :p )

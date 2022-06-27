# Pure-and-mixed-Nash-equilibria-by-maxima-CAS</p>
Finding Nash equilibria
for multiplayer games using Computer Algebra System
(maxima CAS).

Whoever starts to
study game theory, starts to solve many exercises about finding pure
Nash equilibrium in particular models. It is funny at the start but
after one gets the essentials of the process, the process start to
feel very repetitive. In that case, either because the student would
like verification of his manual solution either he wants to avoid
repetition of the same process, it seems nice to let the calculation
to be done by his software. In this repository I use the free and
very nice Computer Algebra System
[maxima](https://maxima.sourceforge.io/index.html) or his equally
very nice graphical interface [wxmaxima](https://wxmaxima-developers.github.io/wxmaxima/).

(The files were created by using exclusively the lovely 'wxmaxima' graphical interface. To acquire the equilibria one does not
actually need the 'wxmaxima' interface and the corresponded .wxmx files. 'wxmaxima' opens maxima's .wxm files.)


<p style="line-height: 100%; margin-bottom: 0cm">The model of the
game is given by a file, in comma separated values format, called
<b>NashData.csv</b></p>
<p style="line-height: 100%; margin-bottom: 0cm">It can be edited by
hand.

**The first row** is a series of numbers where the first one is the
number of players and the next ones gives, sequentially, how many
actions are available to each one of the players. So,</p>
<p style="line-height: 100%; margin-bottom: 0cm">7,8,9,3,6,2,9,6</p>
<p style="line-height: 100%; margin-bottom: 0cm">1,1,1,1,1,1,1,1,2</p>
<p style="line-height: 100%; margin-bottom: 0cm">…</p>
<p style="line-height: 100%; margin-bottom: 0cm">means a 7 players
game, with 8 actions for 1<sup>st</sup> player, 9 for 2<sup>nd</sup>,
3 for 3nd, 6 for 4<sup>th</sup> and so on.</p>

**The second row** inputs possible assumptions. They are usefull if some variable is used in rewards. Leave it as it is "assume( )" or input the assumptions, for examble "assume(c\>0, c\<1)"


**Next rows give the rewards of each player for each profile.**
So, from the example above,
the <b>NashData.csv</b> file should have the first two rows plus other 7(players)
\* (8\*9\*3\*6\*2\*9\*6) (profiles per player) = 7 * 139968 =  979776 rows.
That means exactly 979778 rows. (About 1 million rewards is the
maximum that either 'maxima' or my laptop can handle in about 7 minutes
of calculations. Above that limit, calculations are interrupted with
a message that informs that Lisp can not collect or handle some
garbage data.)

<p style="line-height: 100%; margin-bottom: 0cm">Each row points, by
its first number, to the number of a player, by the rest numbers, excluded
the last one, points to the profile the particular player is facing and
by the last number to the reward that this player has for that
particular profile.  So, with the exception of the first row that has 8 numbers and second row with the assumption string, with 7 players each row, has 9 numbers. (1 for the player, 7 for the
profile and 1 for the reward.)</p>

<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="5" style="font-size: 18pt">Data
input</font></font></p>
A convenient way to input the data is to use maxima to create, excluding the rewards, all other
data automatically. In case that rewards is desirable to include operators or variables, edit last field as string, for examble

1,1,1,"1-1/3" or

1,1,1,"1-c". 

Edit and execute the file <b>Nash_create_data.wxm</b>

Line 60 for the players and their actions and line 65 for the possible assumptions.

The execution will create <span lang="en-US"><b>NashData.csv</b> </span><span lang="en-US">file
with random, 1 digit, rewards.</span>
<p><span lang="en-US">After that, one only needs to replace the 1
digit rewards by the desired ones. In repository exists an edited examble of this file.</span></p>
<p><span lang="en-US">On the basic use, one edits the
  </span><span lang="en-US"><i>Nash_create_data</i> </span><span lang="en-US">file
and gives the 60th row as a list. For the example above the first
row of data should be given as</span></p>
<p><span lang="en-US">n:[</span><span lang="en-US">7,8,9,3,6,2,9,6</span><span lang="en-US">]</span></p>
<p><span lang="en-US">(Alternatively, by commenting the basic 60th row, where ‘n’ list is defined, and un-commenting the 76th and 81th rows,
one can give (in 76th row) only the number of players, for example, as</span></p>
<p><span lang="en-US">N:7</span></p>
<p><span lang="en-US">and the execution of </span><span lang="en-US"><i>Nash_create_data</i>
</span><span lang="en-US">file will create random, from to 2 to 9,
number of actions for each player too.)</span></p>
<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="5" style="font-size: 18pt">Pure
Nash equilibria</font></font></p>
<p>To find pure Nash equilibria one loads the <b>pure_Nash.wxmx</b> by 'wxmaxima' and run it
  or</p>
execute


<p><span lang="en-US"><B>maxima -b ~/pure_Nash.wxm</B></span></p>
<p><span lang="en-US">in a terminal.</span></p>
<p><span lang="en-US">The equilibria are given as a list of pairs of
equilibrium and rewards for this equilibrium lists. For example in</span></p>
<p><span lang="en-US">[[[7, 3, 4], [16, 29, -2]], …]
  
we see that the first equilibrium, in a 3 players’ game, consists of decisions
where 1</span><sup><span lang="en-US">st</span></sup><span lang="en-US">
player chooses his 7</span><sup><span lang="en-US">th</span></sup><span lang="en-US">
action having reward 16, 2</span><sup><span lang="en-US">nd</span></sup><span lang="en-US">
player chooses his 3</span><sup><span lang="en-US">nd</span></sup><span lang="en-US"> having reward 29
and 3nd player chooses his 4</span><sup><span lang="en-US">th </span></sup><span lang="en-US">action having reward -2.</span></p>
<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt">Internally
used process for finding pure strategy equilibria.</font></font></p>
<p>Lucking sufficient knowledge on my hobbies of maths and
programming, I used ‘brutal’ force to acquire the results. I let 'maxima' to create, as strings, sequences of ‘for’
loops and ‘if’ conditions, depending on the number of players and the number of actions that each one has in his disposal.</span></p>
<p><span lang="en-US">The process consist of creating, from the input
data,</span></p>
<p style="line-height: 100%; margin-top: 0.42cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt"><i>the
  R list</i>.</font></font></p>
<p><span lang="en-US">Every element of R consist of two lists</span></p>
<p><span lang="en-US">[list1, [r1,...,r_ak]]</span></p>
<p><span lang="en-US">where list1, on the form of [k, s1,s2, ... (-sk) ...,sn], informs that when player k is facing the si_th action of ith other
player, (-sk) means the profile that does not include the actions of the player himself, gets rewards r1 for his 1st action, r2 for his
2nd and so on till the reward r_ak  for his last available 'ak' action.</span></p>
<p><span lang="en-US">So, [[2,1,2],[17,22]] is from a 3 players game.
It means that the player 2 has two actions, with rewards 17 for his first one and 22 for his second. He gets these rewards when he is facing
the 1st action of player 1 and the 2nd action of player 3 [2,1,2].</span></p>
<p style="line-height: 100%; margin-top: 0.42cm; margin-bottom: 0.21cm; page-break-after: avoid">
  <font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt"><i>The BR list</i></font></font></p>
<p><span lang="en-US">is created from the R list. BR has the same
format as that of list R [list1, list2].</span></p>
<p><span lang="en-US">list1 is the same [k, s1,s2, ... (-sk) ...,sn]
.</span></p>
<p><span lang="en-US">However, list2 consists of the list of indexes
of actions that gives the maximum reward.</span></p>
<p><span lang="en-US">For example if the list of the rewards [r1,...,r_ak] was
[1,3,-2,3] then list2 would be equal to [2,4].</span></p>
<p style="line-height: 100%; margin-top: 0.42cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="4" style="font-size: 14pt"><i>Equilibrium
  criteria</i></font></font></p>
<p>are created as string. Every profile, so every combination of
actions, is checked against Nash equilibrium criteria by executing
that string.</p>


<p align="center" style="line-height: 100%; margin-top: 0.11cm; margin-bottom: 0.21cm; page-break-after: avoid">
<font face="Liberation Sans, sans-serif"><font size="5" style="font-size: 18pt">Mixed
Nash equilibria</font></font></p>
<p>To find mixed Nash equilibria one loads the <b>mixed_Nash.wxm</b> by 'wxmaxima' and run it
  or</p>
execute


<p><span lang="en-US"><B>maxima -b ~/mixed_Nash.wxm</B></span></p>
<p><span lang="en-US">in a terminal.</span></p>
<p><span lang="en-US">The equilibria are given as a list of pairs of
equilibrium (as a list of probabilities) and list of rewards, one for each player, for this equilibrium. 
  
  For the solutions, systems of equations are solved for every possible support and checked the solutions to be real, the probabilities greater than zero or in 'unknown' status and rewards greater or equal to the rewards that are not included in support (have zero probability in mixed strategy). The systems increase rapidly as players or their actions increase. I can not tell the limit of my laptop but, for 4 players with 3 actions the 2 of them and 2 actions the other 2, my laptop needed 3minutes to solve the resulting 7\*3\*7\*3=441 systems. (A set of 3 actions has 7 subsets, except of empty set, and a set of 2 actions has 3 such subsets). 
  
  An example of edited NashData.csv and the relevant outputs are included in present repository.


The mixed equilibria are stored in **Nash** list with each element in the form


[ [[solutions], [conditions]], [rewards] ]
So,

*  Nash[10][2] are the rewards of 10th equilibrium.
*  Nash[10][1][1] are the probabilities of distribution of 10th equilibrium
*  Nash[10][1][2] are the conditions for the 10th equilibrium to be.


**Limitations**
Except from the obvious limitations on memory and on length of strings that are constructed (for the last, specially in pure_Nash.wxm, if it remains as it is), limitations derive also from the main commands (*alg_sys* and *fourier_elim*) that actually find equilibria.
So, if conditions, for example, computed (from *fourier_elim*) as [a1\*a2+a1\*a3+a2\*a3>0, -(a1\*a2+a1\*a3+a2\*a3)>0] one must exclude the solution from equilibria manually, because *fourier_elim* seems it can not find the obvious *empyset* as its solution, so as the relevant equilibrium to be excluded.
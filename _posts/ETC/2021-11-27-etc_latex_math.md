---
defaults:
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      comments: true
      share: true
      related: true

title: "LaTeX 문법 정리"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ETC
tags:
  - [github blog]
date: 2021-11-27
last_modified_at: 2021-11-27
---
<br>

## 1. 그리스 문자

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$\alpha$|\alpha|$\beta$|\beta|$\gamma$|\gamma|$\delta$|\delta|$\epsilon$|\epsilon|
|$\zeta$|\zeta|$\eta$|\eta|$\theta$|\theta|$\iota$|\iota|$\kappa$|\kappa|
|$\lambda$|\lambda|$\mu$|\mu|$\nu$|\nu|$\xi$|\xi|$o$|o (omicron)|
|$\pi$|\pi|$\rho$|\rho|$\sigma$|\sigma|$\tau$|\tau|$\upsilon$|\upsilon|
|$\phi$|\phi|$\chi$|\chi|$\psi$|\psi|$\omega$|\omega|||
|
|$\varepsilon$|\varepsilon|$\vartheta$|\vartheta|$\varkappa$|\varkappa|$\varpi$|\varpi|$\varrho$|\varrho|
|$\varphi$|\varphi|$\varsigma$|\varsigma|
|
|$A$|A (Alpha)|$B$|B (Beta)|$\Gamma$|\Gamma|$\Delta$|\Delta|$E$|E (Epsilon)|
|$Z$|Z (Zeta)|$H$|H (Eta)|$\Theta$|\Theta|$I$|I (Iota)|$K$|K (Kappa)|
|$M$|M (Mu)|$N$|N (Nu)|$\Xi$|\Xi|$O$|O (Omicron)|$\Pi$|\Pi|
|$P$|P (Rho)|$\Sigma$|\Sigma|$T$|T (Tau)|$\Upsilon$|\Upsilon|$\Phi$|\Phi|
|$X$|X (Chi)|$\Psi$|\Psi|$\Omega$|\Omega|

## 2. 폰트

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$\mathcal{A}$|\mathcal{A}|$\mathbb{A}$|\mathbb{A}|$\mathfrak{A}$|\mathfrak{A}|$\mathsf{A}$|\mathsf{A}|$\mathbf{A}$|\mathbf{A}|

## 3. 첨자

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$\acute{a}$|\acute{a}|$\grave{a}$|\grave{a}|$\hat{a}$|\hat{a}|$\check{a}$|\check{a}|$\bar{a}$|\bar{a}|
|$\dot{a}$|\dot{a}|$\ddot{a}$|\ddot{a}|$\tilde{a}$|\tilde{a}|$\vec{a}$|\vec{a}|$\breve{a}$|\breve{a}|
 

## 4. 괄호

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$($|(|$)$|)|$\{$|\{|$\}$|}|$[$|[|
|$]$|]|$\langle$|\langle|$\rangle$|\rangle|$\vert$|\vert|$\Vert$|\Vert|
|$/$|/|$\backslash$|\backslash|$\lfloor$|\lfloor|$\rfloor$|\rfloor|$\lceil$|\lceil|
|$\rceil$|\rceil|$\llcorner$|\llcorner|$\lrcorner$|\lrcorner|$\ulcorner$|\ulcorner|$\urcorner$|\urcorner|


## 5. 화살표 기호

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$\leftarrow$|\leftarrow|$\rightarrow$|\rightarrow|$\uparrow$|\uparrow|$\downarrow$|\downarrow|$\Leftarrow$|\Leftarrow|
|$\Rightarrow$|\Rightarrow|$\Uparrow$|\Uparrow|$\Downarrow$|\Downarrow|$\leftharpoonup$|\leftharpoonup|$\rightharpoonup$|\rightharpoonup|  
|$\upharpoonleft$|\upharpoonleft|$\downharpoonleft$|\downharpoonleft|$\leftharpoondown$|\leftharpoondown|$\rightharpoondown$|\rightharpoondown|$\upharpoonright$|\upharpoonright|
|$\downharpoonright$|\downharpoonright|$\leftleftarrows$|\leftleftarrows|$rightrightarrows\$|\rightrightarrows|$\upuparrows$|\upuparrows|$\downdownarrows$|\downdownarrows|
|$\longleftarrow$|\longleftarrow|$\longrightarrow$|\longrightarrow|$\Lsh$|\Lsh|$\Rsh$|\Rsh|$\Longleftarrow$|\Longleftarrow|
|$\Longrightarrow$|\Longrightarrow|$\leftarrowtail$|\leftarrowtail|$\rightarrowtail$|\rightarrowtail|$\hookleftarrow$|\hookleftarrow|$\hookrightarrow$|\hookrightarrow|
|$\twoheadleftarrow$|\twoheadleftarrow|$\twoheadrightarrow$|\twoheadrightarrow|$\leftrightharpoons$|\leftrightharpoons|$\rightleftharpoons$|\rightleftharpoons|$\curvearrowleft$|\curvearrowleft|
|$\curvearrowright$|\curvearrowright|$\leftrightarrows$|\leftrightarrows|$\rightleftarrows$|\rightleftarrows|$\circlearrowleft$|\circlearrowleft|$\circlearrowright$|\circlearrowright|
|$\Lleftarrow$|\Lleftarrow|$\Rrightarrow$|\Rrightarrow|$\looparrowleft$|\looparrowleft|$\looparrowright$|\looparrowright|$\leftrightarrow$|\leftrightarrow|
|$\Leftrightarrow$|\Leftrightarrow|$\nleftarrow$|\nleftarrow|$\nLeftarrow$|\nLeftarrow|$\longleftrightarrow$|\longleftrightarrow|$\Longleftrightarrow$|\Longleftrightarrow|
|$\nrightarrow$|\nrightarrow|$\nRightarrow$|\nRightarrow|$\updownarrow$|\updownarrow|$\Updownarrow$|\Updownarrow|$\nleftrightarrow$|\nleftrightarrow|
|$\nLeftrightarrow$|\nLeftrightarrow|$\mapsto$|\mapsto |$\longmapsto$|\longmapsto |$\rightsquigarrow$|\rightsquigarrow |$\leftrightsquigarrow$|\leftrightsquigarrow|
|$\swarrow$|\swarrow|$\searrow$|\searrow|$\nwarrow$|\nwarrow|$\nearrow$|\nearrow|


  
## 6. 부등호 기호

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$<$|<|$>$|>|$\$|\nless|$\$|\ngtr|$\$|\leq|
|$\geq$|\geq|$\nleq$|\nleq|$\ngeq$|\ngeq|$\lneq$|\lneq|$\gneq$|\gneq|
|$\leqq$|\leqq|$\geqq$|\geqq|$\nleqq$|\nleqq|$\ngeqq$|\ngeqq|$\nleqq$|\nleqq|
|$\gneqq$|\gneqq|$\leqslant$|\leqslant|$\geqslant$|\geqslant|$\nleqslant$|\nleqslant|$\ngeqslant$|\ngeqslant|
|$\prec$|\prec|$\succ$|\succ|$\nsucc$|\nsucc$|$\vartriangleleft$|\vartriangleleft|$\vartriangleright$|\vartriangleright|
|$\ntriangleleft$|\ntriangleleft|$\ntriangleright$|\ntriangleright|$\trianglelefteq$|\trianglelefteq|$\trianglerighteq$|\trianglerighteq|$\ntrianglelefteq$|\ntrianglelefteq|
|$\ntrianglerighteq$|\ntrianglerighteq|$\eqslantless$|\eqslantless|$\eqslantgtr$|\eqslantgtr|$\ll$|\ll|$\gg$|\gg|
|$\lessgtr$|\lessgtr|$\gtrless$|\gtrless|$\lll$|\lll|$\ggg$|\ggg|$\lesseqgtr$|\lesseqgtr|
|$\gtreqless$|\gtreqless|$\lesseqqgtr$|\lesseqqgtr|$\gtreqqless$|\gtreqqless|$\preccurlyeq$|\preccurlyeq|$\succcurlyeq$|\succcurlyeq|
|$\curlyeqprec$|\curlyeqprec|$\curlyeqsucc$|\curlyeqsucc|



## 7. 관계 기호

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$=$|=|$\$|\neq|$\$|\doteq|$\$|\doteqdot|$\$|\equiv|
|$\$|\not\equiv|$\$|\fallingdotseq|$\$|\risingdotseq|$\sim$|\sim|$\nsim$|\nsim|
|$\triangleq$|\triangleq|$\circeq$|\circeq|$\approx$|\approx|$\not\approx$|\not\approx|$\bumpeq$|\bumpeq|
|$\Bumpeq$|\Bumpeq|$\cong$|\cong|$\ncong$|\ncong|$\simeq$|\simeq|$\approxeq$|\approxeq|
|$\backsim$|\backsim|$\backsimeq$|\backsimeq|$\mid$|\mid|$\nmid$|\nmid|$\parallel$|\parallel|
|$\nparallel$|\nparallel|$\shortmid$|\shortmid|$\nshortmid$|\nshortmid|$\shortparallel$|\shortparallel|$\nshortparallel$|\nshortparallel|
|$\vdash$|\vdash|$\nvdash$|\nvdash|$\vDash$|\vDash|$\nvDash$|\nvDash|$\nVdash$|\nVdash|
|$\Vdash$|\Vdash|$\nVdash$|\nVdash|$\dashv$|\dashv|$\Vvdash$|\Vvdash|

## 8. 집합 기호

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$\subset$|\subset|$\supset$|\supset|$\cap$|\cap|$\cup$|\cup|$\Subset$|\Subset|
|$\Supset$|\Supset|$\Cap$|\Cap|$\Cup$|\Cup|$\sqsubset$|\sqsubset|$\sqsupset$|\sqsupset|
|$\sqcap$|\sqcap|$\sqcup$|\sqcup|$\triangleleft$|\triangleleft|$\triangleright$|\triangleright|$\vartriangle$|\vartriangle|
|$\triangledown$|\triangledown|$\blacktriangleleft$|\blacktriangleleft|$\blacktriangleright$|\blacktriangleright|$\blacktriangle$|\blacktriangle|$\blacktriangledown$|\blacktriangledown|
|$\in$|\in|$\notin$|\notin|$\ni$|\ni|$\subseteq$|\subseteq|$\nsubseteq$|\nsubseteq|
|$\supseteq$|\supseteq|$\nsupseteq$|\nsupseteq|$\subsetneq$|\subsetneq|$\supsetneq$|\supsetneq|$\subseteqq$|\subseteqq|
|$\nsubseteqq$|\nsubseteqq|$\supseteqq$|\supseteqq|$\nsupseteqq$|\nsupseteqq|$\subsetneqq$|\subsetneqq|$\supsetneqq$|\supsetneqq|
|$\sqsubseteq$|\sqsubseteq|$\sqsupseteq$|\sqsupseteq|

## 9. 기타 기호

|수식|Latex|수식|Latex|수식|Latex|수식|Latex|수식|Latex|
|---|---|---|---|---|---|---|---|---|---|
|$+$|+|$-$|-|$\times$|\times|$\div$|\div|$\pm$|\pm|
|$\mp$|\mp|$\setminus$|\setminus|$\between$|\between|$\infty$|\infty|$\propto$|\propto|
|$\therefore$|\therefore|$\because$|\because|$\diagdown$|\diagdown|$\diagup$|\diagup|$\wr$|\wr|
|$\asymp$|\asymp|$\leftthreetimes$|\leftthreetimes|$\rightthreetimes$|\rightthreetimes|$\ltimes$|\ltimes|$\rtimes$|\rtimes|
|$\angle$|\angle|$\measuredangle$|\measuredangle|$\sphericalangle$|\sphericalangle|$\aleph$|\aleph|$\imath$|\imath|
|$\jmath$|\jmath|$\ell$|\ell|$\forall$|\forall|$\exists$|\exists|$\nexists$|\nexists|
|$\neg$|\neg|$\prime$|\prime|$\backprime$|\backprime|$\partial$|\partial|$\emptyset$|\emptyset|
|$\Re$|\Re|$\Im$|\Im|$\mho$|\mho|$\copyright$|\copyright|$\LaTeX$|\LaTeX|
|$\wedge$|\wedge|$\vee$|\vee|$\curlywedge$|\curlywedge|$\curlyvee$|\curlyvee|$\barwedge$|\barwedge|
|$\veebar$|\veebar|$\bigtriangleup$|\bigtriangleup|$\bigtriangledown$|\bigtriangledown|$\frown$|\frown|$\smile$|\smile|
|$\smallfrown$|\smallfrown|$\smallsmile$|\smallsmile|$\cdot$|\cdot|$\circ$|\circ|$\bullet$$|\bullet$|
|$\centerdot$|\centerdot|$\cdots$$|\cdots$|$\vdots$|\vdots|$\ddots$|\ddots|$\ldots$|\ldots|
|$\boxdot$|\boxdot|$\boxplus$|\boxplus|$\boxminus$|\boxminus|$\boxtimes$|\boxtimes|$\odot$|\odot|
|$\oplus$|\oplus|$\ominus$|\ominus|$\otimes$|\otimes|$\oslash$|\oslash|$\circledcirc$|\circledcirc|
|$\circleddash$|\circleddash|$\circledast$|\circledast|$\diamondsuit$|\diamondsuit|$\clubsuit$|\clubsuit|$\heartsuit$|\heartsuit|
|$\spadesuit$|\spadesuit|$\bigcirc$|\bigcirc|$\square$|\square|$\Box $|\Box |$\lozenge $|\lozenge |
|$\Diamond$|\Diamond|$\blacklozenge$|\blacklozenge|$\diamond$|\diamond|$\ast$|\ast|$\star$|\star|
|$\dagger$|\dagger|$\ddagger$|\ddagger|$\sharp$|\sharp|$\flat$|\flat|$\natural$|\natural|
|$\bot$|\bot|$\top$|\top|

<br>


**📌reference**
- [jjycjn's Math Storehouse](https://jjycjnmath.tistory.com/117)
- [wiki LaTeX](https://en.wikibooks.org/wiki/LaTeX/Mathematics)
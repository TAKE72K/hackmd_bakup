# Cadcintest 2021

- alpha submission: 2021/6/11 17:00

- code repo: 

## cad contest problemD
[題目](http://iccad-contest.org/2021/tw/ProblemD-20210429.pdf)
[Q&A](http://iccad-contest.org/2021/tw/Problem%20D_QA_0517.pdf)

## 論文參考
[MP tree](https://sci-hub.se/10.1109/TCAD.2008.927760)
[fast place](http://www.aspdac.com/aspdac2006/archives/pdf/2C-2.pdf)
[contraint graph base](https://sci-hub.se/10.1109/ICCAD.2008.4681577)
[ref](http://www.eng.ucy.ac.cy/theocharides/isvlsi12/isvlsi11/20110704_ywchang_ISVLSI.pdf)

## 進度

- [x] parser
- [ ] data structure(progressing)
- [ ] algorithm


## Worlflow
```flow
st=>start: start
en=>end: exit
op=>operation: parser read DEF, LEF
op2=>operation: sort macros by x cordonate
op3=>operation: try build contour
op4=>operation: exception
cond=>condition: macro placed
cond1=>condition: if all macro placed success?

st->op->op2->op3->cond
cond(yes)->cond1
cond(no)->op4
cond1(no)->op3
cond1(yes)->en

```


## class def

### macro
```c++
class MACRO
{
public:
	MACRO();
	~MACRO();
	float macroW, macroH;
	const char* macroName;
	const char* macroType;
	vector<MACROPIN*> macropins;
	vector<BLOCKAGE*> macro_obs;
};
```
### NETLIST

```c++
class NETLIST
{
public:
	NETLIST() :totalModArea(0), totalStdArea(0), totalPadArea(0), nStd(0), nPad(0),
		nHard(0), nMod(0), nPin(0), nBlockage(0) {};
	~NETLIST() {};
	int ChipBoundary_llx, ChipBoundary_lly, ChipBoundary_urx, ChipBoundary_ury; // chip boundary lower lef xy, upper right xy
	int ChipWidth, ChipHeight;
	float ChipArea;
	float aR;
	float totalModArea, totalStdArea, totalPadArea;
	unsigned int nStd, nPad, nHard, nMod, nPin, nNet, nBlockage;
	vector<PAD> pads;
	vector<MODULE> mods;
	vector<PIN> pins;
	vector<NET> nets;
	vector<BLOCKAGE> blockages;
};

```


### contour
```
class contour
{
    public:
        vector<contour_edge> E;
        build_contour
}
```
```
class contour's edge
{
    point start;
    point end;
    macro* touched;
}
```


# memo



## 説明

CHOP Executeの今回の中身が以下. 

- onSwitchOn: 負から正に変わったタイミングで実行される

- whileOn: 正の間はずっと実行される

- onSwitchOff: 正から負に変わったタイミングで実行される

- whileOff: 負の間はずっと実行される

この関数内に記述しても, CHOP Executeのinspector内でその関数をOnにしてあげないと実行されないので注意. 



`sayHello` のような自作関数を書いても単体では実行されない. 

ただし, デフォルトの関数 (上記4関数) の中で使用すれば, 自作関数も実行される. 



b'abc' はpythonのバイト型のこと. Asciiとして各文字に対応した数字に変換される. 
したがって, a=97, b=98, c=99となる. 





## code

```python
# me - this DAT
# 
# channel - the Channel object which has changed
# sampleIndex - the index of the changed sample
# val - the numeric value of the changed sample
# prev - the previous sample value
# 
# Make sure the corresponding toggle is enabled in the CHOP Execute DAT.

def onSwitchOn(channel, sampleIndex, val, prev):
	n= op('oscout1')
  
	# vals = [1, b'abc', 'apple', [6,7,8], str(absTime.frame), None, float("infinity")]
	vals = [1, 2, "hoge", 'hoge', [1], b'!0abc~', str(absTime.frame)]
	# b'abc' is byte type. it sends a number by ascii format
	n.sendOSC('/abc', vals)
	return

def whileOn(channel, sampleIndex, val, prev):
	n= op('oscout1')  
	vals = [str(absTime.frame)]
	n.sendOSC('/abc', vals)
	return

def onSwitchOff(channel, sampleIndex, val, prev):
	sendValues()
	return

def whileOff(channel, sampleIndex, val, prev):
	return

def onValueChange(channel, sampleIndex, val, prev):
	return
	
def sayHello(channel, sampleIndex, val, prev):
	return

def sendValues():
	n= op('oscout1')
	vals = [1234578901234567890, "hoge", 'hoge', [1], b'abc', str(absTime.frame)]
	n.sendOSC('/abc', vals)
	return
```


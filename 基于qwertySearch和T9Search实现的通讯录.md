###基于qwertySearch 和 T9Search实现的通讯录

作者简书地址：[http://www.jianshu.com/p/3c54cc71e238](http://www.jianshu.com/p/3c54cc71e238)

官方github地址：[https://github.com/handsomezhou/PinyinSearchLibrary](https://github.com/handsomezhou/PinyinSearchLibrary)

我的github地址：	[https://github.com/yin13753884368/qwertySearch](https://github.com/yin13753884368/qwertySearch)

####Function call in detail:

	Import packages when use PinyinSearch Library(Dependent on pinyin4j-x.x.x.jar):
	import com.pinyinsearch.util.*;
	import com.pinyinsearch.model.*;
	
	The first step:  Data parsing  (ps:Must init baseData of PinyinSearchUnit before parse)
	    * (PinyinUtil.parse(...))
	The second step: Data matching 
	    * (T9Util.match(...) or QwertyUtil.match(...))
	
	For details, please see project ContactsSearch and AppSearch.

####使用要点：

	//1.用Searcy初始化 PinyinSearchUnit
	namePinyinSearchUnit = new PinyinSearchUnit(itemWordName);
	//2.初始化 初始化之前先new PinyinSearchUnit
	PinyinUtil.parse(namePinyinSearchUnit);
	//3.去匹配，输出汉字
		if (headName.contains(lowerCase.substring(0, 1))) {
			if (QwertyUtil.match(namePinyinSearchUnit, text)) {//search by name;
			string = namePinyinSearchUnit.getMatchKeyword().toString();
			//将要改变颜色的字体设置到bean
			itemCont.setColorName(string);
			// Log.d("call", "查	询...namePinyinSearchUnit===" + string + "....lowerCase===" + lowerCase + "..." + text);
			list.add(itemCont);
		
		}


####使字体改变颜色

		/**
	     * 使字体变色
	     * @param baseText
	     * @param highlightText if the string of highlightText is a subset of the string of baseText,highlight the string of highlightText.
	     */
	    public void showTextHighlight(String baseText, String highlightText) {
	
	        if (baseText != null && highlightText != null && highlightText.length() > 0) {
	
	            int index = baseText.indexOf(highlightText);
	            if (index < 0) {
	                this.setText(baseText);
	                return;
	            }
	
	            int len = highlightText.length();
	            /**
	             *  "<u><font color=#FF8C00 >"+str+"</font></u>"; 	//with underline
	             *  "<font color=#FF8C00 >"+str+"</font>";			//without underline
	             *  //将颜色设置成蓝色
	             *  <color name="dark_orange">#FF8C00</color>
	             */
	            Spanned spanned = Html.fromHtml(baseText.substring(0, index) + "<font color=#38ADFF >"
	                    + baseText.substring(index, index + len) + "</font>"
	                    + baseText.substring(index + len, baseText.length()));
	
	            this.setText(spanned);
	        } else {
	            this.setText(baseText);
	        }  
	    }
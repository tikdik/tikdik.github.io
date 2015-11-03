#Intent意图系统
##explicit(明确) intent

	Intent intent= new Intent(this, MyActivity.class)； 

明确指定了组件是MyActivity

	public Intent(Context context, Class<?> cls) {
		mCompenent = new CompenontName(context, cls);
	}

从Intent实例化可以看出，explicit intent就是明确指定要去启动哪个基本组件

##implicit(隐藏) intent

需要进行三个匹配，一个是action，一个是category，一个是data

###action

出发动作

###category

action是比较大到范围， 需要细化分类， 只有分类intent-filter包含了请求intent里面到category，这个组件才能接收。

如果intent仅仅包含了action,android默认会加入android.intent.category.DEFAULT，所以如果组件需要接收某种action，必须加上android.intent.category.DEFAULT，但有种会例外，就是

	<intent-filter>  
        <action android:name="android.intent.action.MAIN" />  
        <category android:name="android.intent.category.LAUNCHER" />  
    </intent-filter> 

###data
当有data时，需要至少匹配其中一种data数据，同时针对该action,同时是里面的一种类别category
比如
    
    <intent-filter >
        <action android:name="android.intent.action.VIEW"/>
        <category android:name="android.intent.category.BROWSABLE"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="image/*"/>
    </intent-filter>

这时可用如下代码启动，里面需要针对这个action，同时针对了android.intent.category.DEFAULT类

    Intent intent = new Intent(Intent.ACTION_VIEW);
    intent.setDataAndType(Uri.fromFile(new File("/sdcard/DCIM/P51101-170827.jpg")), "image/*");
    startActivity(intent);



####scheme

scheme://host:port/path or pathPrefix or pathPattern

####mimeType

多用途互联网邮件扩展（MIME，Multipurpose Internet Mail Extensions）是一个互联网标准，它扩展了电子邮件标准，使其能够支持非ASCII字符、二进制格式附件等多种格式的邮件消息。

说白了就是处理文件格式，具体支持哪些参考这个标准

通过Uri来标识

    Uri uri = Uri.parse("tel:13888888888");
    intent.setAction(Intent.ACTION_VIEW);
    intent.setData(uri);
    startActivity(intent);

示例：

    <activity android:name="com.android.gallery3d.app.MovieActivity"
            android:label="@string/movie_view_label"
            android:configChanges="orientation|keyboardHidden|screenSize">
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="rtsp" />
         </intent-filter>
         <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="http" />
            <data android:scheme="https" />
            <data android:scheme="content" />
            <data android:scheme="file" />
            <data android:mimeType="video/mpeg4" />
            <data android:mimeType="video/mp4" />
            <data android:mimeType="video/3gp" />
            <data android:mimeType="video/3gpp" />
            <data android:mimeType="video/3gpp2" />
            <data android:mimeType="video/webm" />
            <data android:mimeType="video/avi" />
            <data android:mimeType="application/sdp" />
            <data android:mimeType="video/mp2ts" />
            <data android:mimeType="video/x-ms-asf" />
            <data android:mimeType="video/x-ms-wmv" />
            <data android:mimeType="video/x-matroska" />
            <data android:mimeType="video/x-msvideo"/>
            <data android:mimeType="video/divx" />
            <data android:mimeType="video/mkv" />
            <data android:mimeType="video/mpeg" />
         </intent-filter>
         <intent-filter>
            <!-- HTTP live support -->
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="http" />
            <data android:scheme="https" />
            <data android:mimeType="audio/x-mpegurl" />
            <data android:mimeType="audio/mpegurl" />
            <data android:mimeType="application/vnd.apple.mpegurl" />
            <data android:mimeType="application/x-mpegurl" />
            <data android:mimeType="application/dash+xml" />
         </intent-filter>
    </activity>
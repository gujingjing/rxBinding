####什么是rxBinding
rxBinding是一个开源库，让你可以以raJava的形式来处理ui事件。

######1. rxBinding的点击事件
举个栗子，rxBinding可以监听view的点击事件

		//点击事件的绑定
				RxView.clicks(tvClick)
						.throttleFirst(1000, TimeUnit.SECONDS)   //两秒钟之内只取一个点击事件，防抖操作
						.subscribe(new Action1<Void>() {
					@Override
					public void call(Void aVoid) {
						Toast.makeText(MainActivity.this,"点击了",Toast.LENGTH_SHORT).show();
					}
				});
				//lamb表达式书写
				RxView.clicks(tvClick)
						.throttleFirst(1000, TimeUnit.SECONDS)   //两秒钟之内只取一个点击事件，防抖操作
						.subscribe(aVoid -> {
							Toast.makeText(MainActivity.this,"点击了",Toast.LENGTH_SHORT).show();
						});


注意:Edittext使用RxTextView,其他的view使用RxView

例子:监听按钮的长按

		//button的长按的监听
				RxView.longClicks(btnLongClick).subscribe(aVoid -> {
					Toast.makeText(MainActivity.this, "长按了", Toast.LENGTH_SHORT).show();
				});

例子:监听checkBox的选中情况

		//CheckBox的监听
				RxCompoundButton.checkedChanges(ckChoose).subscribe(aBoolean -> {
					tvCkViewShow.setText(aBoolean?"选中了":"没有被选中");
				});




例子:edittext的监听

		//edittext内容的监听
				RxTextView.textChangeEvents(tvEdittext)
						.debounce(600, TimeUnit.MILLISECONDS)//debounce是在600毫秒内没有操作就发生事件
						.subscribe(new Action1<TextViewTextChangeEvent>() {
							@Override
							public void call(TextViewTextChangeEvent textViewTextChangeEvent) {
								tvEditViewShow.setText(textViewTextChangeEvent.text());
							}
						});
				RxTextView.textChangeEvents(tvEdittext)
						.debounce(600, TimeUnit.MILLISECONDS)//debounce是在600毫秒内没有操作就发生事件
						.subscribe(textViewTextChangeEvent -> {
							tvEditViewShow.setText(textViewTextChangeEvent.text());
						});

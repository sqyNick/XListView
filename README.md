# XListView
##本工程将开源的XListView控件提取出来，方便自己自定义header跟footer

使用方式：将.java文件跟.xml文件拷贝到对应的地方，自定义的话更改相应布局即可
```java
       <com.fhzz.cn.exploremap.view.XListView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:id="@+id/date_query_listview"
            android:divider="@null"
            >
        </com.fhzz.cn.exploremap.view.XListView>
```
1.设置下拉刷新,上拉加载更多是否开启
```java
        listView.setPullRefreshEnable(false);
        listView.setPullLoadEnable(true);
```
2.加载监听
```java
      listView.setXListViewListener(new XListView.IXListViewListener() {

            @Override
            public void onRefresh() {

            }

            @Override
            public void onLoadMore() {
                List<ExplorePoint> points=DBUtil.getPointByPage(pointLists.size(), 10,submitStatus );
                if(points != null && points.size()>0)
                {
                    pointLists.addAll(points);
                    adapter.notifyDataSetChanged();
                }else {
                    Toast.makeText(getBaseContext(), "没有更多数据", Toast.LENGTH_SHORT).show();
                    listView.setPullLoadEnable(false);
                }
                listView.stopLoadMore();
            }
        });
```


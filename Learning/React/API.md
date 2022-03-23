環境テストどうしよう｡

express環境は開発環境設定できるかどうか｡



Api 

質問：

区別

rest.v1.bean

rest.v2.bean

rest.v3.bean



apiviewmanager





Binder binder = BRD.*getBinderFactory*().loadBinder(_binder.getIdLong());

​    SmartCabinet cabinet = binder.getSmartCabinet();



​    // バインダに登録されているすべてのテーブルビューを一覧する

​    TableViewFactory tvf = cabinet.getManager().getTableViewFactory();

​    List<TableView> allViews = tvf.getAllViews(cabinet, *ViewGroup*.***NORMAL_DOC_VIEW\***);
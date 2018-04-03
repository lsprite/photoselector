#使用方法
---
private ArrayList<String> result = new ArrayList<>();
/**
*MAX_PHOTO_SUM最大选择照片数量
*COLUMN_COUNT一行显示照片数
*/
 private void selectPhotos(int sum, int columnCount) {
        PhotoSelectorSetting.MAX_PHOTO_SUM = sum;
        PhotoSelectorSetting.COLUMN_COUNT = columnCount;
        Intent intent = new Intent(MainActivity.this, PhotoSelectorActivity.class);
        intent.putExtra(PhotoSelectorSetting.LAST_MODIFIED_LIST, result);
        startActivityForResult(intent, REQUEST_SELECT_PHOTO);
}

 @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        switch (requestCode) {
            case REQUEST_SELECT_PHOTO:
                if (resultCode == RESULT_OK) {
                    result = data.getStringArrayListExtra(PhotoSelectorSetting.LAST_MODIFIED_LIST);
                    boolean isSelectedFullImage = data.getBooleanExtra(PhotoSelectorSetting.SELECTED_FULL_IMAGE, false);
                    photoRecyclerViewAdapter.setList(result, isSelectedFullImage);
                }
                break;
        }
    }
---
	<activity
            android:name="com.fire.photoselector.activity.PhotoSelectorActivity"
            android:configChanges="orientation|screenSize"
            android:screenOrientation="portrait" />
	<activity
            android:name="com.fire.photoselector.activity.PhotoViewActivity"
            android:configChanges="orientation|screenSize"
            android:screenOrientation="portrait" />
            
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
            
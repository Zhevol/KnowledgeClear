
### 1、生命周期定义

　　Activity 的生命周期是需要熟悉的，其生命周期的各个方法必须熟悉。同时，对常见应用场景下的生命周期，也是需要熟记的。以下是一张 Activity 的生命周期图。

   ![Activity生命周期图](/pictures/Activity生命周期.png)

   为了弄清楚这张图，首先要清楚 Activity 可能存在的三种状态：

   - 继续　此 Activity 处于屏幕前台并具有焦点；
   - 暂停　此 Activity 处于被其他 Activity 部分覆盖的状态，但是仍可见，此 Activity 不具有焦点。
   - 停止　此 Activity 处于被其他 Activity 完全覆盖的状态，并且不可见，此 Activity 目前位于后台。

   其次，在实现及调用 Activity 的各个生命周期方法的时候，需要使用 `super.onXxx()` 方法调用父类实现。
   在上图的 Activity 的生命周期具有三个嵌套循环：

   - `onCreate()` 和 `onDestroy()` 循环：Activity 的**整个生命周期**发生在这两者的调用之间。通常在 `onCreate()` 中执行布局的设置及相关全局信息的设置；在 `onDestroy()` 中进行数据销毁、释放资源等操作。
   - `onStart()` 和 `onStop()` 循环：Activity 的**可见生命周期**发生在这两者的调用之间。在此期间用户可以在屏幕上看到此 Activity 并与其交互。
   - `onResume()` 和 `onPause()` 循环：Activity 的**前台生命周期**发生在这两者的调用之间。在此期间，此 Activity 显示在屏幕上并具有焦点。

   各个生命周期的回调方法汇总信息表：

   <table>
       <tr>
         <th colspan="1"><h4>方法</h4></th>
         <th colspan="1"><h4>说明</h4></th>
         <th colspan="1"><h4>是否能事后终止</h4></th>
         <th colspan="1"><h4>后接</h4></th>
       </tr>
       <tr>
             <td><code>onCreate()</code></td>
             <td><code>首次创建 Activity 时调用。 您应该在此方法中执行所有正常的静态设置 — 创建视图、将数据绑定到列表等等。 系统向此方法传递一个 Bundle 对象，其中包含 Activity 的上一状态，不过前提是捕获了该状态。<br/>始终后接 onStart()。</code></p></td>
             <td><code>否</code></td>
             <td><code>onStart()</code></td>
       </tr>

   </table>
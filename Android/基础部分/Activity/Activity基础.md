
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
             <td>onCreate()</td>
             <td>首次创建 Activity 时调用。 您应该在此方法中执行所有正常的静态设置 — 创建视图、将数据绑定到列表等等。 系统向此方法传递一个 Bundle 对象，其中包含 Activity 的上一状态，不过前提是捕获了该状态。<br/>始终后接 onStart()。</td>
             <td>否</td>
             <td>onStart()</td>
       </tr>
       <tr>
             <td>onRestart()</td>
             <td>在 Activity 已停止并即将再次启动前调用。<br/>始终后接 onStart()。</td>
             <td>否</td>
             <td>onStart()</td>
       </tr>
       <tr>
             <td>onStart()</td>
             <td>在 Activity 即将对用户可见之前调用。<br/>如果 Activity 转入前台，则后接 onResume()，如果 Activity 转入隐藏状态，则后接 onStop()。</td>
             <td>否</td>
             <td>onResume() 或 onStop()</td>
       </tr>
       <tr>
             <td>onResume()</td>
             <td>在 Activity 即将开始与用户进行交互之前调用。 此时，Activity 处于 Activity 堆栈的顶层，并具有用户输入焦点。<br/>始终后接 onPause()。</td>
             <td>否</td>
             <td>onPause()</td>
       </tr>
       <tr>
             <td>onPause()</td>
             <td>当系统即将开始继续另一个 Activity 时调用。 此方法通常用于确认对持久性数据的未保存更改、停止动画以及其他可能消耗 CPU 的内容，诸如此类。 它应该非常迅速地执行所需操作，因为它返回后，下一个 Activity 才能继续执行。<br/>如果 Activity 返回前台，则后接 onResume()，如果 Activity 转入对用户不可见状态，则后接 onStop()。</td>
             <td>是</td>
             <td>onResume() 或 onStop()</td>
       </tr>
       <tr>
             <td>onStop()</td>
             <td>在 Activity 对用户不再可见时调用。如果 Activity 被销毁，或另一个 Activity（一个现有 Activity 或新 Activity）继续执行并将其覆盖，就可能发生这种情况。<br/>如果 Activity 恢复与用户的交互，则后接 onRestart()，如果 Activity 被销毁，则后接 onDestroy()。</td>
             <td>是</td>
             <td>onRestart() 或 onDestroy()</td>
       </tr>
       <tr>
             <td>onDestroy()</td>
             <td>在 Activity 被销毁前调用。这是 Activity 将收到的最后调用。 当 Activity 结束（有人对 Activity 调用了 finish()），或系统为节省空间而暂时销毁该 Activity 实例时，可能会调用它。 您可以通过 isFinishing() 方法区分这两种情形。</td>
             <td>是</td>
             <td>无</td>
       </tr>
   </table>
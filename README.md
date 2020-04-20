# Uni Display Progress Bar Scope

* EditorUtility.ClearProgressBar の呼び出し漏れを防ぐためのクラス  
* using に対応しているため、プログレスバー表示中に例外が発生してもプログレスバーを非表示にしてくれます   

## 使用例

```cs
using System.Collections;
using Unity.EditorCoroutines.Editor;
using UnityEditor;
using UnityEngine;

public static class Example
{
    [MenuItem( "Tools/Hoge" )]
    private static void Hoge()
    {
        EditorCoroutineUtility.StartCoroutineOwnerless( Test() );
    }

    private static IEnumerator Test()
    {
        var count = 100;

        using ( var bar = new DisplayProgressBarScope( "Title", "Progress: {0}" ) )
        {
            for ( var i = 0; i < count; i++ )
            {
                bar.Progress = ( float ) i / count;

                yield return new WaitForSeconds( 0.1f );
            }
        }
    }
}
```
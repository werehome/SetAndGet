# Set/Get(Use SetProperty)
Unity allows you to serialize private fields with [SerializeField]. Use the new [SetProperty] attribute to have a public property set every time the field is modified in Unity's inspector.
## Example
	[SerializeField, SetProperty("Number")]
	private float number;
	public float Number
	{
    	get
    	{
			return number;
    	}
			private set
    	{
			number = Mathf.Clamp01(value);
    	}
	}
		
#Another solution
Put this code in the directory.  
		
	using UnityEngine;
	using UnityEditor;
	using System.Collections.Generic;  
	    
	[CustomEditor(typeof(Test))]
	public class TestInspector : Editor  
	{
		Test model;
		public override void OnInspectorGUI()
		{
			model=target as Test;
			int width=EditorGUILayout.IntField("Width",model.width);
			if(model.width!=width)
			{
				model.width=width;
			}
			base.DrawDefaultInspector();
		}
	}  
			
And put this code on the game object.  
		
	using UnityEngine;
	using System.Collections;
 
	public class Test : MonoBehaviour 
	{
		public int width
		{
			get 
			{
				return _width; 
			}
			set 
			{
				Debug.Log("set :" + value);
				_width = value; 
			}
		}
		private int _width;
	}  
		
In edit mode,use the mouse to change the value of width.

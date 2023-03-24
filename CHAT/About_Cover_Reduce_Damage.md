> Me: 
> ```
> Unity 3D How to know character behind and forward on sanbag using collision example
> ```
> GPT:
> * Sure! Here's an example of how to use collision detection to detect objects behind and in front of a sandbag in Unity 3D:
> * Add a script to the sandbag object. This script should include two methods, one to detect objects in front of the sandbag and one to detect objects behind the sandbag:
```
public class SandbagScript : MonoBehaviour
{
    private GameObject objectInFrontOfSandbag;
    private GameObject objectBehindSandbag;

    private void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            if (other.gameObject.transform.position.z > transform.position.z)
            {
                objectInFrontOfSandbag = other.gameObject;
            }
            else if (other.gameObject.transform.position.z < transform.position.z)
            {
                objectBehindSandbag = other.gameObject;
            }
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.gameObject.CompareTag("Player"))
        {
            if (other.gameObject.transform.position.z > transform.position.z)
            {
                objectInFrontOfSandbag = null;
            }
            else if (other.gameObject.transform.position.z < transform.position.z)
            {
                objectBehindSandbag = null;
            }
        }
    }

    public GameObject GetObjectInFrontOfSandbag()
    {
        return objectInFrontOfSandbag;
    }

    public GameObject GetObjectBehindSandbag()
    {
        return objectBehindSandbag;
    }
}
```
> * This script uses OnTriggerEnter and OnTriggerExit to detect when objects collide with the sandbag.
> * If the colliding object is a player and is in front of or behind the sandbag, the script stores a reference to the object in the objectInFrontOfSandbag or objectBehindSandbag variables, respectively. 
> * The script also includes two methods to return the objects in front of or behind the sandbag.
> * Attach the script to the sandbag object in your game.
> * Create a reference to the sandbag script in the character script:
```
public class CharacterScript : MonoBehaviour
{
    private SandbagScript sandbagScript;

    private void Start()
    {
        sandbagScript = GameObject.Find("Sandbag").GetComponent<SandbagScript>();
    }

    private void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            GameObject objectInFrontOfSandbag = sandbagScript.GetObjectInFrontOfSandbag();
            if (objectInFrontOfSandbag != null)
            {
                Debug.Log("Object in front of sandbag: " + objectInFrontOfSandbag.name);
            }

            GameObject objectBehindSandbag = sandbagScript.GetObjectBehindSandbag();
            if (objectBehindSandbag != null)
            {
                Debug.Log("Object behind sandbag: " + objectBehindSandbag.name);
            }
        }
    }
}
```
> * In the character script's Update method, check for a mouse click and call the sandbag script's GetObjectInFrontOfSandbag and GetObjectBehindSandbag methods. If an object is detected in front of or behind the sandbag, log the name of the object to the console.
> * Run the game and click on the sandbag to see the names of the objects behind and in front of it in the console.
> * Note that this is just an example and may need to be adapted to fit the specifics of your game. Additionally, this method assumes that the sandbag is always facing the character and the objects behind and in front of the sandbag are directly in front of and behind it, respectively.
> * If this is not the case, you may need to adjust the detection logic to get accurate results.
## Build and test

Now it's time to make your marble mayhem experience. Start small and then add more if you have time.

Image, gif or video showing what they will achieve by the end of the step. ![](images/image.png)

### Unity reference

[[[unity-editor]]]

[[[unity-projects-scenes]]]

[[[unity-scene-navigation]]]

[[[unity-scene-top-down]]]

### Create your level

[[[unity-3D-coordinates]]]

[[[unity-transform-tools]]]

[[[unity-plane]]]

[[[unity-vertex-snapping]]]

[[[unity-scene-gizmo]]]

**Tip:** If you are using one of the 'Floor' GameObjects from the asset package, make sure to select all the 'Cube' child objects and add a Box Collider component to them.

### Add your marble

--- task ---

Add a Sphere GameObject and rename it to `Marble`. 

Scale the ball to fit your project.

--- /task ---

--- task ---

Add a material for your marble.

[[[unity-transform-tools]]]
[[[unity-existing-material]]]
[[[unity-material-with-texture]]]
[[[unity-glass-material]]

--- /task ---

--- task ---

Add a Rigidbody to your marble. 

[[[unity-rigidbody]]]

--- /task ---

**Choose**

Control your marble directly with the keyboard.

or 

Tilt the level to roll your marble around. 

[[[unity-control-ball]]]

[[[unity-tilt-world]]]

[[[unity-keyboard-conventions]]]

### Set up your camera

**Choose:** The view you want to use for your project. 

If the player is controlling the ball with the keyboard you will want to choose a view behind and a little above the ball like this...

![The camera view behind and just above the ball, perfect for a game where the camera follows the ball.](images/camera-view.png)

To tilt the world you should first switch to top view. 

[[[unity-scene-top-down]]]

This will make sure the camera is facing the right way for the tilt mechanic. You might want to rotate the camera to X=`80`, Y=`0`, Z=`0`. 

Align the camera to the Scene view.

[[[unity-align-with-view]]]

**Choose:** Whether the camera will follow the marble or not. 

If you are controlling the marble with the keyboard you will want the camera to follow. 

For the Tilt you can leave the camera zoomed out and not have it follow the marble - or zoom in and set up the CameraFollow script. 

[[[unity-camera-follow-ball]]]

You might also want to be able to rotate the camera. 

**Tip:** Do not do this if you are tilting the level as it will mess up the orientation. 

[[[unity-rotate-camera-mouse]]]

### Play and test

Press the Play button and test your game so far. 

Check that you are happy with the following things: 
- The layout of your level
- Camera view, angle and controls
- Marble or world tilt controls
- The difficulty of your level without obstacles

**Debug:** 
- Make sure you exit Play mode before making any changes as they will not be saved if changed during Play mode

### Obstacles

Now it is time to add some obstacles for the marble to interact with! 

**Choose:** Here are some ideas for obstacles that you could add to your project. 

- Bouncy obstacles to get in the way of the marble, like the Capsules in Rainbow Run and Track Designer
- Spinning obstacles
- Objects or Floor tiles that fall away when the marble rolls over them

You can use any of the models included in your starter package or make your own out of simple GameObjects. 

--- collapse ---

---
title: Make objects spin
---

Add your GameObject into the Scene and change it's position and rotation until you are happy with it. 

In the Inspector click **'Add Component'** and add the `Spin` script. 

If you do not have the `Spin` script, create a new script called `Spin` and place it in your 'Scripts' folder. 

Open the script and type or copy the following code into the editor. 

--- code ---
---
language: cs
filename: Spin.cs
line_numbers: true
line_number_start: 
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Spin : MonoBehaviour
{
    public Vector3 rotation;

    // Update is called once per frame
    void Update()
    {
        transform.Rotate(rotation * Time.deltaTime);
    }
}

--- /code ---

Save your script and switch back to the Unity editor. 

In the Inspector add a value to the `Rotation` variable in any of the X, Y or Z axes. 

![The Spin component with 50 set in the Y section of Rotation.](images/spin-component.png)

--- /collapse ---

--- collapse ---

---
title: Make obstacles that fall
---

Add your GameObject into the Scene and change it's position and rotation until you are happy with it. 

In the Inspector click **'Add Component'** and add a `Rigidbody` component.

Make sure to set 'Use Gravity' to False and 'Is Kinematic' to True. 

![The Rigidbody component with the variables described above set.](images/rigidbody-fall-set-up.png)

Add a new script called `Fall`, place it in your 'Scripts' folder. 

Open the script and type or copy the following code into the editor. 

--- code ---
---
language: cs
filename: Fall.cs
line_numbers: true
line_number_start: 
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Fall : MonoBehaviour
{    
    void OnCollisionEnter(Collision collision) {
        if (collision.gameObject.tag == "Player"){
            GetComponent<Rigidbody>().useGravity = true;
            GetComponent<Rigidbody>().isKinematic = false;
        }
    }
}

--- /code ---

Save your script, and switch back to the Unity editor.

**Tip:** Make sure to tag your marble as "player" for the script to work.

--- /collapse ---

### Physics Materials

You can add Physics Materials to all the objects in your Scene to change the ways objects collide. 

**Choose:** Which objects to add Physics Materials and what the attributes of the Physics Materials are. 

- The marble
- The obstacles 
- Pieces of the level. 

Physics Materials have three attributes that you can set to any value between `0` and `1` to change an objects interactions: 
**Dynamic Friction:** How quickly an object that is already moving will slow down. `0` is like ice (not very much friction) and `1` would stop a moving object very quickly. 
**Static Friction:** The amount of force needed to move an object from standing still. `0` means not a lot of force is needed and `1` would require a huge amount of force to move an object. 
**Bounciness:** How bouncy an object is. `0` is no bounce at all and `1` means an object will bounce and not lose any velocity.

[[[bouncy-material]]]

Create some Physics materials and add them to objects in your Scene.

### Materials, sounds and effects

Now it is time to add the final touches to your Scene. 

**Choose:** You can add code to your objects to do any of the following: 
- Change material when colliding with the player
- Change to a random colour on collision
- Play a sound on collision
- Play a sound when the player enters an area
- Add a particle effect when the player enters an area

You can use the Scripts you have created during the pathway for these effects, if you don't have the scripts you can find them below. 

**Tip:** Make sure that your marble is tagged as "Player" for these to work.

--- collapse ---

---
title: Change to a specific Material
---

--- code ---
---
language: cs
filename: ChangeMaterial.cs
line_numbers: true
line_number_start: 
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ChangeMaterial : MonoBehaviour
{
    public Material newMaterial;

    void OnCollisionEnter(Collision collision) {
        if (collision.gameObject.tag == "Player"){
            GetComponent<Renderer>().sharedMaterial = newMaterial;
        }
    }
}

--- /code ---

--- /collapse ---

--- collapse ---

---
title: Change to a random colour
---

--- code ---
---
language: cs
filename: RandomColour.cs
line_numbers: true
line_number_start: 
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class RandomColour : MonoBehaviour
{
    void OnCollisionEnter(Collision other) {
        if (other.gameObject.CompareTag("Player")){
            Color NewColor = Random.ColorHSV(0f, 1f, 1f, 1f, 0.5f, 1f);
            gameObject.transform.GetComponent<MeshRenderer>().material.color = NewColor;
        }
    }
}

--- /code ---

--- /collapse ---

--- collapse ---

---
title: Play a sound
---

--- code ---
---
language: cs
filename: PlaySound.cs
line_numbers: true
line_number_start: 
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlaySound : MonoBehaviour
{
    AudioSource audioSource;
    
    // Start is called before the first frame update
    void Start()
    {
        audioSource = GetComponent<AudioSource>();
    }

    // Check for collisions with the player
    void OnCollisionEnter(Collision other)
    {
        if (other.gameObject.CompareTag("Player")){
            audioSource.Play();
        }
    }
}

--- /code ---

**Tip:** You will need to add an `AudioSource` component to the object for this to work, set it so it does not 'Play on Awake' and add a Sound file to the 'Clip' section in the Inspector.

--- /collapse ---

--- collapse ---

---
title: Start an effect
---

--- code ---
---
language: cs
filename: PlayEffect.cs
line_numbers: true
line_number_start: 
line_highlights: 
---

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FinishEffects : MonoBehaviour
{
    ParticleSystem completeParticleSystem;
    
    // Start is called before the first frame update
    void Start()
    {
        completeParticleSystem = GetComponentInChildren<ParticleSystem>();
    }

    // Update is called once per frame
    void OnCollisionEnter(Collision other)
    {
        if (other.gameObject.tag == "Player"){
            completeParticleSystem.GetComponent<ParticleSystemRenderer>().material = other.gameObject.GetComponent<Renderer>().material;
            completeParticleSystem.Play();
        }
    }
}

**Tip:** You will need to add the 'Fireworks' GameObject from your assets as a child of the GameObject. 

--- /code ---

--- /collapse ---

### Play and test

Play your game to test out all your new features to check they are working how you expect. 

Fix any bugs you find. 

**Debug:**


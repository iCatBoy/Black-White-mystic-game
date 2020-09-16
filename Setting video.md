using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class SettingVideo : MonoBehaviour
{
    public Toggle fullScreenToggle;
    public Dropdown resolutionDropdown;
    Resolution[] resolutions;
    void Start()
    {

        resolutions = Screen.resolutions;
        resolutionDropdown.ClearOptions();
        List<string> options = new List<string>();
        int currentResolutionIndex = 0;
        for (int i = 0; i < resolutions.Length; ++i)
        {
            string option = resolutions[i].width + "x" + resolutions[i].height + " " + resolutions[i].refreshRate + "Hz";
            options.Add(option);
            if ((resolutions[i].width == Screen.width) &&
                (resolutions[i].height == Screen.height) &&
                (resolutions[i].refreshRate == Screen.currentResolution.refreshRate))
            {
                currentResolutionIndex = i;
            }
        }
        resolutionDropdown.AddOptions(options);
        resolutionDropdown.value = currentResolutionIndex;
        resolutionDropdown.RefreshShownValue();
        fullScreenToggle.isOn = Screen.fullScreen;
    }
    public void SetResolution(int resolutionIndex)
    {
        Resolution resolution = resolutions[resolutionIndex];
        Screen.SetResolution(resolution.width, resolution.height, Screen.fullScreen,resolution.refreshRate);
        Text txt;
        txt = GameObject.Find("Canvas/Text").GetComponent<Text>();
        txt.text = "resolution.refreshRate : " + resolution.refreshRate ;
    }
    public void SetQuality(int qualityIndex)
    {
        QualitySettings.SetQualityLevel(qualityIndex);
    }
    public void SetFullscreen(bool isFullscreen)
    {
        Screen.fullScreen = isFullscreen;

    }
}

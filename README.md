using UnityEngine;
using MscModApi; // MscModApi library

public class OilCoolerMod : MonoBehaviour
{
    private float oilTemperature = 80f;
    private readonly float maxOilTemperature = 100f;
    private readonly float coolingEfficiency = 0.9f;
    private bool installedOnCar = false;

    // Mod properties
    public string ModID => "OilCoolerMod";
    public string ModName => "Oil Cooler";
    public string ModAuthor => "RPM";
    public string ModVersion => "1.1.0";
    public string ModDescription => "This mod installs an oil cooler to prevent engine overheating.";

    // Method to install the oil cooler
    public void InstallOilCooler()
    {
        if (!installedOnCar)
        {
            installedOnCar = true;
            Debug.Log("Oil cooler installed on the car.");

            // Action to reduce the oil temperature
            oilTemperature = Mathf.Max(oilTemperature - (coolingEfficiency * 10f), 70f);
            UpdateOilTemperatureDisplay();
        }
    }

    // Method to remove the oil cooler
    public void RemoveOilCooler()
    {
        if (installedOnCar)
        {
            installedOnCar = false;
            Debug.Log("Oil cooler removed from the car.");

            // Action to increase the oil temperature
            oilTemperature = Mathf.Min(oilTemperature + (coolingEfficiency * 15f), maxOilTemperature);
            UpdateOilTemperatureDisplay();
        }
    }

    // Update the oil temperature display
    private void UpdateOilTemperatureDisplay()
    {
        Debug.Log($"Oil temperature: {oilTemperature}°C");
    }

    // Monitor the oil temperature
    private void MonitorOilTemperature()
    {
        if (installedOnCar)
        {
            if (oilTemperature > maxOilTemperature)
            {
                oilTemperature = Mathf.Max(oilTemperature - (coolingEfficiency * 5f), maxOilTemperature);
            }
        }
        else
        {
            oilTemperature = Mathf.Min(oilTemperature + 0.1f, maxOilTemperature);
        }

        UpdateOilTemperatureDisplay();
    }

    // Update method called every frame
    private void Update()
    {
        MonitorOilTemperature(); // Monitoring the oil temperature
    }

    // Method called when the game starts
    private void Start()
    {
        // Mod initialization
        Debug.Log("Oil cooler mod loaded.");
        oilTemperature = 80f; // Initial oil temperature
    }
}
